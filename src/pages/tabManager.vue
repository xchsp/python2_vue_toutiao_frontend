<template>
  <div>
    <headerMiddle title="栏目管理" />
    <div class="Active">
      <h2 class="title">点击删除以下频道</h2>
      <div
        :key="index"
        @click="toDeactive(index)"
        class="tab"
        v-for="(item,index) in tabActive"
      >{{item.name}}</div>
    </div>
    <div class="Deactive">
      <h2 class="title">点击添加以下频道</h2>
      <div
        :key="index"
        @click="toActive(index)"
        class="tab"
        v-for="(item,index) in tabDeactive"
      >{{item.name}}</div>
    </div>
  </div>
</template>

<script>
import headerMiddle from '@/components/HeaderMiddle'

export default {
  components: {
    headerMiddle
  },
  data() {
    return {
      tabActive: [],
      tabDeactive: []
    }
  },
  watch: {
    tabActive() {
      localStorage.setItem('tabActive', JSON.stringify(this.tabActive))
    },
    tabDeactive() {
      localStorage.setItem('tabDeactive', JSON.stringify(this.tabDeactive))
    }
  },
  methods: {
    toDeactive(index) {
      if (this.tabActive.length == 2) {
        this.$notify({
          type: 'danger',
          message: '请保留2个选项',
          duration: 2000
        })
        return
      }
      this.tabDeactive.push(this.tabActive[index])
      this.tabActive.splice(index, 1)
    },
    toActive(index) {
      this.tabActive.push(this.tabDeactive[index])
      this.tabDeactive.splice(index, 1)
    },
    getTabs() {
              this.$axios({
                url:'/category',
                method:'get'
              }).then(res=>{
                  // console.log(res)
                  res.forEach(element=>{
                      element.currentPageIndex = 1
                      element.posts = []
                      element.finished = false
                  })
                  this.tabActive = res
                  console.log(res)

              })
    }
  },
  mounted() {
    if (
      localStorage.getItem('tabActive') &&
      localStorage.getItem('tabDeactive')
    ) {
      this.tabActive = JSON.parse(localStorage.getItem('tabActive'))
      this.tabDeactive = JSON.parse(localStorage.getItem('tabDeactive'))
    } else {
      this.getTabs()
    }
  }
}
</script>

<style lang="less" scoped>
.Active,
.Deactive {
  padding: 8/@vv;
  height: 40vh;
  .title {
    font-weight: normal;
    margin-bottom: 8/@vv;
    font-size: 20/@vv;
  }
  .tab {
    width: 45/@vv;
    text-align: center;
    float: left;
    margin: 4/@vv 8/@vv;
    background-color: #f6f6f6;
    border: 1px solid #eee;
  }
}
</style>
