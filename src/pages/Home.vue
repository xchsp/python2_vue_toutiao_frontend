<template>
    <div>
        <homeHeader></homeHeader>
        <van-tabs sticky v-model="activeTab">
          <van-tab :key="index" v-for="(tabItem,index) in tabList" :title="tabItem.name">
            <van-list
            v-model="loading"
            :finished="tabItem.finished"
            finished-text="没有更多了"
            :immediate-check = "false"
            @load="loadMorePosts"
            >
              <post v-for="(item,index) in tabItem.posts" :key="index" :post="item"></post>
            </van-list>
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
            loading:false,
            // finished:false,
            activeTab:0,
            // posts: [],
            tabList:[],
            pageSize:5
          }
        },
        watch:{
          activeTab(newTab){
            console.log(newTab)
            if(this.tabList[newTab].posts.length==0)
            {
              this.getTabPosts(newTab)
            }

          }
        },
        mounted(){
          this.initTabList()
        },
        methods:{
          loadMorePosts(){
            console.log('loadMorePosts')
            this.tabList[this.activeTab].currentPageIndex+=1
            this.getTabPosts(this.activeTab)
          },
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
                  // let arr1 = [1,2,3,4]
                  // let arr2 = ['zhagnsan','lisi']
                  // let arr12 = [...arr1,...arr2]
                  // console.log(arr12)
                  let postsArray = [...this.tabList[tabIndex].posts,...res.data]
                  this.tabList[tabIndex].posts = postsArray
                  if(res.data.length < this.pageSize){
                      this.tabList[tabIndex].finished = true
                  }
                  console.log(res)
              })
          },
          initTabList(){
              if(localStorage.getItem('tabActive')){
                this.tabList = JSON.parse(localStorage.getItem('tabActive'))
                this.getTabPosts(this.activeTab)
                return
              }

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
