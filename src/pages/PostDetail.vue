<template>
      <div>
        <div class="mainContent">
        <div class="title">{{post.title}}</div>
        <video
          :poster="post.cover[0].url"
          class="video"
          controls="controls"
          src="https://video.pearvideo.com/mp4/adshort/20191031/cont-1618052-14544566_adpkg-ad_sd.mp4"
          v-if="post.type==2"
        ></video>
        <div class="info" v-if="post.user">{{post.user.nickname}} 2019-10-31</div>
        <div class="content" v-html="post.content" v-if="post.type!=2"></div>
        <div class="actionBtn">
          <div class="like">
            <span :class="{red: post.has_like}" @click="like" class="iconfont icondianzan"></span>
            {{post.like_length}}
          </div>
          <div class="webchat">
            <span class="iconfont iconweixin"></span>
            <a
              href="https://developers.weixin.qq.com/doc/offiaccount/Getting_Started/Explanation_of_interface_privileges.html"
            >微信</a>
          </div>
        </div>
        <div class="commentList">
          <h2 class="title">精彩跟帖</h2>
          <div v-if="post.comment_length==0">
            <div>暂无跟帖,抢占沙发</div>
          </div>
          <comment
          v-else
          v-for="(item,index) in comments"
          :key="index"
          :commentItem="item"
          >
          </comment>

          <div class="more">
            <div @click="toMoreComments" class="moreComment">更多跟帖</div>
          </div>
        </div>
      </div>

        <postDetailFooter
      :post="post"
      @newComment="getComments"
      >

      </postDetailFooter>
      </div>

</template>

<script>
     import postDetailFooter from '@/components/postDetailFooter'
     import comment from '@/components/comment'
    export default {
        name: "PostDeatail",
        components:{
          postDetailFooter,
          comment
        },
        data(){
          return {
            comments:[],
            post:{},
            postId:this.$route.params.id
          }
        },
        mounted(){
              this.$axios({
                url:'/post/' + this.postId,
                method:'get'
              }).then(res=>{
                  console.log(res)
                  this.post = res
                  this.getComments()
              })
        },
        methods:{
          getComments(){
              this.$axios({
                url:'/get_comments/' + this.postId,
                method:'get',
                params:{
                  pageSize:3
                }
              }).then(res=>{
                  console.log(res)
                  this.comments = res
              })
          },
          toMoreComments(){
                this.$router.push({
                    name: 'moreComments',
                    params: {
                      id: this.postId
                    }
                  })
          },
          like(){

          }
        }
    }
</script>

<style lang="less" scoped>
.mainContent {
  padding-bottom: 80/@vv;
  padding-left: 10px;
  padding-right: 10px;
  .info {
    margin: 8/@vv 0;
  }
  .content {
    width: 375/@vv;
    /deep/ img {
      width: 100%;
      height: 200/@vv;
      object-fit: cover;
    }
  }
  .video {
    width: 100%;
    margin: 8/@vv 0;
  }
  .actionBtn {
    padding: 30/@vv 0;
    display: flex;
    justify-content: space-around;
    border-bottom: 5/@vv solid #e4e4e4;
    color: #333;
    .like {
      padding: 6/@vv 18/@vv;
      text-align: center;
      background-color: #ddd;
      border-radius: 14/@vv;
      font-size: 14px;
    }
    .webchat {
      padding: 6/@vv 12/@vv;
      text-align: center;
      background-color: #ddd;
      border-radius: 14/@vv;
      font-size: 14px;
      .iconweixin {
        color: #00c800;
      }
    }
  }
  .commentList {
    padding: 20px 0;
    .title {
      text-align: center;
      font-weight: normal;
      color: #666;
      font-size: 20px;
    }
  }
  .more {
    padding-top: 30px;
    text-align: center;
    .moreComment {
      width: 80px;
      padding: 4px 14px;
      margin: 0 auto;
      border-radius: 14px;
      font-size: 14px;
      border: 1px solid #888;
      color: #666;
      background-color: #eee;
    }
  }
}
.red {
  color: #f00;
}
</style>
