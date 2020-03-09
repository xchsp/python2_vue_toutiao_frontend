<template>
  <div class="container">
    <div @click="jumpPage" class="user">
      <label for>{{label}}</label>
      <div class="desc">
        {{desc}}
        <span class="iconfont iconjiantou1"></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['label', 'desc'],
  methods: {
    jumpPage() {
      this.$emit('click')
    }
  }
}
</script>

<style lang="less" scoped>
.container {
  padding-left: 20/@vv;
}
.user {
  display: flex;
  justify-content: space-between;
  height: 60/@vv;
  line-height: 60/@vv;
  border-bottom: 1px solid #eee;
}
</style>
