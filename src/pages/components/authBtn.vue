<template>
    <div class="btn" @click="handleClick">{{text}}</div>
</template>

<script>
    export default {
        props:['text'],
        methods:{
          handleClick(event){
            this.$emit('clickxx')
          }
        }
    }
</script>

<style lang="less" scoped>
.btn {
  width: 250/@vv;
  height: 48/@vv;
  line-height: 48/@vv;
  color: #fff;
  background-color: #cc3300;
  border-radius: 24/@vv;
  text-align: center;
}
</style>
