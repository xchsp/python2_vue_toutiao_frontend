<template>
    <div>
      <HeaderMiddle title="编辑资料"></HeaderMiddle>
      <div class="avatar">
        <img :src="profile.head_img" alt class="avatar-img">
        <van-uploader :after-read="afterRead" />
      </div>
    </div>
</template>

<script>
   import HeaderMiddle from '@/components/HeaderMiddle'
    export default {
        name: "EditProfile",
        components:{
          HeaderMiddle
        },
        data(){
          return {
            profile:{}
          }
        },
          methods:{
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
                this.profile = res
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
