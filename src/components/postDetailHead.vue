<template>
  <div class="head">
    <div @click="$router.back()" class="left">
      <span class="iconfont iconjiantou2"></span>
      <span class="iconfont iconnew"></span>
    </div>
    <span @click="follow" class="follow" v-if="!post.has_follow">关注</span>
    <span @click="unfollow" class="alfollow" v-if="post.has_follow">已关注</span>
  </div>
</template>

<script>
export default {
  props: ['post'],
  methods: {
    follow() {
       this.$axios({
            url:'/user_follow/' + this.post.user.id,
            method:'POST',
          }).then(res=>{
            console.log(res)
            if(res.message=='关注成功'){
              this.post.has_follow = true
            }
            else if(res.message=='不能关注自己'){
              this.$toast.fail(res.message)
            }
          })
    },
    unfollow() {
        this.$axios({
            url:'/user_follow/' + this.post.user.id,
            method:'POST',
          }).then(res=>{
           if(res.message=='取消关注成功'){
              this.post.has_follow = false
            }
          })
    }
  }
}
</script>

<style lang="less" scoped>
.head {
  padding: 0 10/@vv;
  display: flex;
  justify-content: space-between;
  align-items: center;
  .left {
    display: flex;
    align-items: center;
    .iconjiantou2 {
      font-size: 15px;
    }
    .iconnew {
      font-size: 54px;
    }
  }
  .follow {
    width: 58/@vv;
    height: 8/@vv;
    padding: 8/@vv 4/@vv;
    line-height: 8/@vv;
    text-align: center;
    font-size: 12px;
    background-color: #f00;
    color: #fff;
    border-radius: 16/@vv;
  }
  .alfollow {
    width: 58/@vv;
    height: 8/@vv;
    padding: 8/@vv 4/@vv;
    line-height: 8/@vv;
    text-align: center;
    font-size: 12px;
    background-color: #eee;
    color: #888;
    border-radius: 16/@vv;
  }
}
</style>
