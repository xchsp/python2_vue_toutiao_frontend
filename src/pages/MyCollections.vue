<template>
    <div class="container">
      <HeaderMiddle title="我的收藏"></HeaderMiddle>
      <post v-for="(item,index) in collectionsList" :key="index" :post="item"></post>
    </div>
</template>

<script>
    import HeaderMiddle from '@/components/HeaderMiddle'
    import post from '@/components/post'
    export default {
        name: "MyCollections",
       components: {
          post,
          HeaderMiddle
        },
       data() {
          return {
            collectionsList: []
          }
       },
          methods: {
            getData() {
              this.$axios({
                url: '/user_star',
                method: 'GET'
              }).then(res => {
                console.log(res)
                this.collectionsList = res
              })
            }
          },
          mounted() {
            this.getData()
        }
    }
</script>

<style lang="less" scoped>
.singleCover {
  display: flex;
  padding: 20/@vv;
  border-bottom: 1px solid #eee;
  .left {
    width: 66%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 0 8/@vv 0 0;
    .info {
      margin-top: 20/@vv;
      color: #888;
      font-size: 14px;
    }
  }
  .right {
    width: 34%;
    height: 74/@vv;
    overflow: hidden;
    img {
      width: 100%;
      height: auto;
      object-fit: cover;
    }
  }
}
.multipCover {
  padding: 20/@vv;
  border-bottom: 1px solid #eee;
  .cover {
    display: flex;
    justify-content: space-between;
    margin-top: 8/@vv;
    .imgWrapper {
      width: 32%;
      height: 74/@vv;
      overflow: hidden;
      img {
        width: 100%;
        height: auto;
        object-fit: cover;
      }
    }
  }
  img {
    width: 112/@vv;
    height: 74/@vv;
  }
}
</style>
