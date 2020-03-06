<template>
  <div>
    <!-- 视频播放器模板 -->
    <div class="videoPost" v-if="post.type ==2">
      <div @click="toPostDetail" class="title">{{post.title}}</div>
      <div @click="toPostDetail" class="cover">
        <img alt class="imgRight" v-lazy="$fixImgUrl(post.cover[0].url)" />
        <div class="btnPlay">
          <span class="iconfont iconshipin"></span>
        </div>
      </div>
      <div class="info">{{post.user.nickname}} {{post.comment_length}}跟帖</div>
    </div>

    <div class="single" v-else-if="post.cover.length >0 && post.cover.length <3">
      <div class="left">
        <div @click="toPostDetail" class="title">{{post.title}}</div>
        <div class="info">{{post.user.nickname}} {{post.comment_length}}跟帖</div>
      </div>
      <img @click="toPostDetail" class="imgRight" v-lazy="$fixImgUrl(post.cover[0].url)" />
    </div>

    <div class="multip" v-else-if="post.cover.length >=3">
      <div @click="toPostDetail" class="title">{{post.title}}</div>
      <div class="cover">
        <!-- 实现懒加载 -->
        <img
          :key="index"
          @click="toPostDetail"
          alt
          v-for="(img,index) in 3"
          v-lazy="$fixImgUrl(post.cover[index].url)"
        />
      </div>
      <div class="info">{{post.user.nickname}} {{post.comment_length}}跟帖</div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['post'],
  methods: {
    toPostDetail() {
      this.$router.push({
        name: 'postDetailPage',
        params: {
          id: this.post.id
        }
      })
    }
  }
}
</script>

<style lang="less" scoped>
.single {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10/@vv;
  border-bottom: 1px solid #eee;
  .left {
    flex: 1;
    height: 75/@vv;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    .title {
      display: -webkit-box;
      -webkit-box-orient: vertical;
      -webkit-line-clamp: 2;
      overflow: hidden;
    }
    .info {
      color: #888;
      font-size: 14px;
    }
  }
  .imgRight {
    width: 121/@vv;
    height: 75/@vv;
    object-fit: cover;
  }
}
.multip {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 10/@vv;
  border-bottom: 1px solid #eee;
  .title {
    flex: 1;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 2;
    overflow: hidden;
  }
  .info {
    color: #888;
    font-size: 14/@vv;
  }
  .cover {
    margin: 10/@vv 0;
    img {
      width: 32%;
      height: 75/@vv;
      margin-right: 4/@vv;
      object-fit: cover;
    }
  }
}
.videoPost {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 10/@vv;
  border-bottom: 1px solid #eee;
  .title {
    flex: 1;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 2;
    overflow: hidden;
  }
  .info {
    color: #888;
    font-size: 14/@vv;
  }
  .cover {
    position: relative;
    margin: 10/@vv 0;
    .btnPlay {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      .iconshipin {
        width: 55/@vv;
        height: 55/@vv;
        line-height: 55/@vv;
        border-radius: 50%;
        text-align: center;
        background: #ccc;
        color: #fff;
        font-size: 40px;
      }
    }
    img {
      width: 100%;
      height: 170/@vv;
      object-fit: cover;
    }
  }
}
</style>
