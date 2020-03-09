<template>
  <div>
    <HeaderMiddle title="我的跟帖"></HeaderMiddle>
    <comment :commentItem="item" :key="index" v-for="(item,index) in comments" />
  </div>
</template>

<script>
import comment from '@/components/comment'
import HeaderMiddle from '@/components/HeaderMiddle'
export default {
  components: {
    comment,
    HeaderMiddle
  },
  data() {
    return {
      comments: []
    }
  },
  methods: {

    getComments() {
      this.$axios({
        url: '/user_comments',
        method: 'get'
      }).then(res => {
        console.log(res)
        this.comments = res
      })
    }
  },
  mounted() {
      this.getComments()
  }
}
</script>

<style>
</style>
