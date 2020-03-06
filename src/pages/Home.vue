<template>
    <div>
        <homeHeader></homeHeader>
        <van-tabs v-model="activeTab">
          <van-tab :key="index" v-for="(tabItem,index) in tabList" :title="tabItem.name">
              <post v-for="(item,index) in tabList[activeTab].posts" :key="index" :post="item"></post>
          </van-tab>
        </van-tabs>
    </div>

</template>

<script>
    import homeHeader from '@/components/homeHeader'
    import post from '@/components/post'
    export default {
        name: "Home",
        components:{
          homeHeader,
          post
        },
        data(){
          return{
            activeTab:0,
            // posts: [],
            tabList:[],
            pageSize:5
          }
        },
        watch:{
          activeTab(newTab){
            console.log(newTab)
            this.getTabPosts(newTab)
          }
        },
        mounted(){
          this.initTabList()
        },
        methods:{
          getTabPosts(tabIndex){
              let cateId = this.tabList[tabIndex].id
              console.log(cateId)
              this.$axios({
                url:'/get_cate_posts',
                method:'get',
                params:{
                  category:cateId,
                  pageIndex:this.tabList[tabIndex].currentPageIndex,
                  pageSize:this.pageSize
                }
              }).then(res=>{
                  this.tabList[tabIndex].posts = res.data
                  console.log(res)
              })
          },
          initTabList(){
              this.$axios({
                url:'/category',
                method:'get'
              }).then(res=>{
                  // console.log(res)
                  res.forEach(element=>{
                      element.currentPageIndex = 1
                      element.posts = []
                  })
                  this.tabList = res
                  console.log(res)
                  this.getTabPosts(this.activeTab)
              })
          }
        }
    }
</script>

<style scoped>

</style>
