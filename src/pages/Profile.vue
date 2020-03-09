<template>
    <div>
      <headerMiddle title="个人中心" />
      <div class="profile">
        <img :src="profile.head_img" @click="$router.push('/editProfile')" alt class="avatar" />
        <div class="profile-middle">
          <div>
            <span class="iconfont iconxingbienan" v-if="profile.gender ==1"></span>
            <span class="iconfont iconxingbienv" v-else></span>
            {{profile.username}}
          </div>
          <div class="time">{{profile.created}}</div>
        </div>
        <span class="iconfont iconjiantou1"></span>
      </div>

      <cellBar @click="$router.push('/myFollow')" label="我的关注" desc="关注的用户"></cellBar>
      <cellBar @click="$router.push('/myComments')" desc="我的跟帖" label="跟帖/回复"></cellBar>
      <cellBar @click="$router.push('/myCollections')" desc="我的收藏" label="文章/视频"></cellBar>
      <cellBar @click="$router.push('/tabManager')" label="栏目管理"></cellBar>
      <cellBar @click="$router.push('/editProfile')" label="设置"></cellBar>
      <cellBar @click="$router.replace('/login')" label="退出"></cellBar>
    </div>
</template>

<script>
    import cellBar from '@/components/cellBar'
    import headerMiddle from '@/components/HeaderMiddle'
    export default {
        name: "Profile",
        components:{
          cellBar,
          headerMiddle
        },
        data(){
          return {
            profile:{}
          }
        },
        methods:{
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
.profile {
  display: flex;
  align-items: center;
  padding: 40/@vv 0;
  border-bottom: 5/@vv solid #eee;
}
.avatar {
  margin-left: 20/@vv;
  width: 70/@vv;
  height: 70/@vv;
  border-radius: 50%;
}
.profile-middle {
  flex: 1;
  padding: 0 20/@vv;
  font-size: 14/@vv;
}
.iconxingbienan {
  margin: 0 4/@vv;
  color: skyblue;
}
.time {
  margin-top: 4/@vv;
  font-size: 14/@vv;
}
</style>
