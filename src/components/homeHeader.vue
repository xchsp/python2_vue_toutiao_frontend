<template>
  <div class="header">
    <span class="iconfont iconnew"></span>
    <div @click="$router.push('/search')" class="search">
      <span class="iconfont iconsearch"></span>
      搜索新闻
    </div>
    <span @click="$router.push('/profile')" class="iconfont iconwode"></span>
  </div>
</template>

<script>
export default {}
</script>

<style lang="less" scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 10/@vv;
  height: 49/@vv;
  background-color: #ff0000;
  color: #fff;
}
.search {
  width: 210/@vv;
  height: 34/@vv;
  line-height: 34/@vv;
  text-align: center;
  border-radius: 17/@vv;
  margin: 0 auto;
  background-color: rgba(242, 242, 242, 0.5);
}
.iconnew {
  font-size: 54px;
}
.iconwode {
  font-size: 20px;
}
</style>
