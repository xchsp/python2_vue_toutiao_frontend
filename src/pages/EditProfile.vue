<template>
    <div>
      <HeaderMiddle title="编辑资料"></HeaderMiddle>
      <div class="avatar">
        <img :src="profile.head_img" alt class="avatar-img">
        <van-uploader :after-read="afterRead" />
      </div>
      <cellBar @click="isShowUsername=true" label="昵称" :desc="profile.username"></cellBar>
      <cellBar @click="isShowPwd=true" label="密码" desc="******"></cellBar>
      <cellBar @click="isShowGender=true" label="性别":desc="profile.gender"></cellBar>

      <van-dialog
        v-model="isShowUsername"
        title="编辑昵称"
        @confirm="editProfile({username:new_user_name})"
        show-cancel-button>
          <van-field v-model="new_user_name" placeholder="请输入用户名" focus="true"/>
      </van-dialog>

       <van-dialog
        v-model="isShowPwd"
        title="编辑密码"
        @confirm="editProfile({password:new_pwd})"
        show-cancel-button>
          <van-field v-model="new_pwd" placeholder="请输入用户名" type="password" focus="true"/>
      </van-dialog>

      <van-action-sheet
            v-model="isShowGender"
            :actions="genderLst"
            cancel-text="取消"
            @select="selectGender"
        />
    </div>


</template>

<script>
   import HeaderMiddle from '@/components/HeaderMiddle'
    import cellBar from '@/components/cellBar'
    export default {
        name: "EditProfile",
        components:{
          HeaderMiddle,
          cellBar
        },
        data(){
          return {
            genderLst:[{name:'男'},{name:'女'}],
            profile:{},
            isShowUsername:false,
            isShowPwd:false,
            isShowGender:false,
            new_user_name:'',
            new_pwd:''
          }
        },
          methods:{
          selectGender(event){
              this.editProfile({gender:(event.name=='男'?1:0)})
              this.isShowGender = false
          },
          afterRead(file){
              let data = new FormData()
              data.append('file',file.file)
              this.$axios({
                url: '/upload/',
                method: 'post',
                data
              }).then(res => {
                console.log(res)
                this.editProfile({head_img:res.data.url})
              })
          },
          editProfile(newInfo){
             this.$axios({
                url: '/update_user',
                method: 'post',
                data:newInfo
              }).then(res => {
                console.log(res)
                this.new_user_name = ''
                this.new_pwd = ''
                this.profile = res
                this.profile.gender = (this.profile.gender == 0 ? '女':'男')
                if(!this.profile.head_img){
                  this.profile.head_img='https://p3.pstatp.com/list/190x124/pgc-image/Rft0hGGCLk6YgJ'
                }
                else{
                  this.profile.head_img = this.$fixImgUrl(this.profile.head_img)
                }
              })
          },
          getData(){
              this.$axios({
                url: '/me',
                method: 'GET'
              }).then(res => {
                console.log(res)
                this.profile = res
                if(!this.profile.head_img){
                  this.profile.head_img='https://p3.pstatp.com/list/190x124/pgc-image/Rft0hGGCLk6YgJ'
                }
                else{
                  this.profile.head_img = this.$fixImgUrl(this.profile.head_img)
                }

                this.profile.gender = (this.profile.gender == 0 ? '女':'男')
              })
          }
        },

        mounted(){
          this.getData()
        }
    }
</script>

<style lang="less" scoped>

  .avatar {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
    position: relative;

    .avatar-img {
      display: block;
      width: 100/@vv;
      height: 100/@vv;
      border-radius: 50%;
    }
    // 修改元素的大小
    /deep/.van-uploader__upload {
      width: 100/@vv;
      height: 100/@vv;
    }
    /deep/.van-uploader {
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
      opacity: 0;
    }
  }
</style>
