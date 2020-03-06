<template>
     <div class="footer">
    <div class="disable" v-if="!isFocus">
      <input @focus="showArea" placeholder="写跟帖" type="text" />
      <div class="comment">
        <span class="iconfont iconpinglun-"></span>
        <div class="commentNumber">{{post.comment_length}}</div>
      </div>
      <span :class="{red: post.has_star}" @click="star" class="iconfont iconshoucang"></span>
      <a
        href="https://developers.weixin.qq.com/doc/offiaccount/Getting_Started/Explanation_of_interface_privileges.html"
      >
        <span class="iconfont iconfenxiang"></span>
      </a>
    </div>
    <div class="enable" v-if="isFocus">
      <textarea @blur="handleBlur" ref="commentArea" rows="3" v-model="comment"></textarea>
      <span @click="send" class="send">发送</span>
    </div>
  </div>
</template>
<script>
    export default {
        name: "postDetailFooter",
        props:['post'],
        data(){
          return {
            isFocus:false,
            comment:''
          }
        },
        methods:{
          send(){
              this.$axios({
                url:'/create_comment/' + this.post.id,
                method:'post',
                data:{
                  content:this.comment
                }
              }).then(res=>{
                  console.log(res)
              })
          },
          star(){

          },
          showArea(){
              this.isFocus = true;
              this.$nextTick(()=>{
                this.$refs.commentArea.focus()
              })

          },
          handleBlur(){

          }
        }
    }
</script>

<style lang="less" scoped>
.footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  .disable {
    display: flex;
    justify-content: space-around;
    align-items: center;
    padding: 10/@vv 10/@vv 10/@vv 0;
    .iconfont {
      font-size: 23/@vv;
    }
    input {
      height: 31/@vv;
      line-height: 31/@vv;
      font-size: 14/@vv;
      border: none;
      outline: none;
      border-radius: 16/@vv;
      padding: 0 16/@vv;
      background-color: #d7d7d7;
      color: #848484;
    }
    .comment {
      position: relative;
      .commentNumber {
        position: absolute;
        left: 2/@vv;
        top: -8/@vv;
        height: 16/@vv;
        line-height: 16/@vv;
        box-sizing: border-box;
        font-size: 12/@vv;
        color: #fff;
        background: #f00;
        border-radius: 8/@vv;
        padding: 0 8/@vv;
      }
    }
  }
  .enable {
    display: flex;
    justify-content: space-around;
    align-items: flex-end;
    padding: 10/@vv 10/@vv 10/@vv 0;
    textarea {
      width: 270/@vv;
      padding: 16/@vv 0;
      box-sizing: border-box;
      border: none;
      outline: none;
      border-radius: 8/@vv;
      color: #666;
      background-color: #d7d7d7;
      resize: none;
    }
    .send {
      padding: 0 15/@vv;
      height: 26/@vv;
      line-height: 26/@vv;
      text-align: center;
      background-color: #f00;
      color: #fff;
      border-radius: 16/@vv;
      border: 1px solid #f00;
      font-size: 14px;
    }
  }
  .red {
    color: #f00;
  }
}
</style>
