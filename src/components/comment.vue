<template>
  <div>
    <div class="commentWraper">
      <div class="meta">
        <img alt class="avatar" src="/static/imgs/default.png" />
        <div class="info">
          <div class="name" v-if="commentItem.user">{{commentItem.user.nickname}}</div>
          <span class="time">{{commentItem.created}}</span>
        </div>
      </div>
      <div class="content">{{commentItem.content}}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['commentItem'],

  data() {
    return {

    }
  },
  methods: {

  }
}
</script>
<style lang="less" scoped>
.commentWraper {
  padding: 10/@vv;
  border-bottom: 1px solid #eee;
  .meta {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 10px;
    .avatar {
      width: 35/@vv;
      height: 35/@vv;
      border-radius: 50%;
      object-fit: cover;
    }
    .info {
      flex: 1;
      padding-left: 10/@vv;
      .time {
        font-size: 14px;
        color: #888;
      }
    }
    /*.btnApply {*/
      /*font-size: 14px;*/
      /*color: #888;*/
    /*}*/
    .avatar {
      width: 50/@vv;
      height: 50/@vv;
      border-radius: 50%;
      object-fit: cover;
    }
  }
  .content {
    margin-top: 20/@vv;
  }
}
</style>
