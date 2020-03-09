<template>
  <div>
    <div class="search">
      <span @click="back" class="iconfont iconjiantou2"></span>
      <div class="searchText">
        <span class="iconfont iconsearch"></span>
        <input class="searchInput" placeholder="请输入搜索内容" type="text" v-model="searchStr" />
      </div>
      <div @click="search" class="btn">搜索</div>
    </div>
    <!-- 渲染内容 -->
    <div v-if="resultList.length>0">
      <post :key="index" :post="post" v-for="(post,index) in resultList"></post>
    </div>
    <div class="content" v-else>
      <div class="history">
        <h3 class="title">历史记录</h3>
        <span
          :key="index"
          @click="searchByWord(item)"
          v-for="(item,index) in historyList"
        >{{item}}&nbsp;</span>
      </div>
      <div class="hot">
        <h3 class="title">热门搜索</h3>
        <span
          :key="index"
          @click="searchByWord(item)"
          v-for="(item,index) in hotList"
        >{{item}}&nbsp;</span>
      </div>
    </div>
  </div>
</template>

<script>
import post from '@/components/post'

export default {
  components: {
    post
  },
  data() {
    return {
      searchStr: '',
      resultList: [],
      historyList: localStorage.getItem('historyList')
        ? JSON.parse(localStorage.getItem('historyList'))
        : [],
      hotList: []
    }
  },
  watch: {
    searchStr() {
      if (this.searchStr == '') {
        // 清空搜索框显示历史记录和热门搜索
        this.resultList = []
        console.log(this.historyList)
      }
    },
    historyList() {
      localStorage.setItem('historyList', JSON.stringify(this.historyList))
      console.log(this.historyList)
    }
  },
  methods: {
    searchByWord(item) {
      this.searchStr = item
      this.search()
    },
    getHotList() {
      this.hotList = ['关晓彤', '女歌手', '王祖贤']
    },
    back() {
      if (this.searchStr) {
        this.searchStr = ''
      } else {
        this.$router.back()
      }
    },
    search() {
      this.$axios({
        url: '/post_search',
        method: 'get',
        params: {
          keyword: this.searchStr
        }
      }).then(res => {
        // const { data } = res.data
        this.resultList = res
        if (this.historyList.indexOf(this.searchStr) < 0) {
          this.historyList.push(this.searchStr)
        }
      })
    }
  },
  mounted() {
    this.getHotList()
  }
}
</script>

<style lang="less" scoped>
.search {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8/@vv;
  .searchText {
    height: 30/@vv;
    border-radius: 15/@vv;
    padding: 0 8/@vv;
    border: 1px solid #ccc;
    .searchInput {
      height: 100%;
      width: 200/@vv;
      border: none;
      outline: none;
    }
  }
  .btn {
    padding: 0 4/@vv;
  }
}

.content {
  .history,
  .hot {
    border-bottom: 1px solid #888;
    height: 200/@vv;
    padding-top: 15/@vv;
    font-size: 14/@vv;
  }
  .history {
    .title {
      margin-bottom: 8/@vv;
    }
  }
  .hot {
    .title {
      margin-bottom: 8/@vv;
    }
  }
}
</style>
