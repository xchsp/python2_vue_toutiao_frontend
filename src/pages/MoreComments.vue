<template>
  <div>
    <HeaderMiddle title="更多跟帖"></HeaderMiddle>
    <comment :commentItem="item" :key="index" v-for="(item,index) in comments" />
    <postDetailFooter
      :post="post"
      @newComment="getComments"
    />
  </div>
</template>

<script>
import postDetailFooter from '@/components/postDetailFooter'
import comment from '@/components/comment'
import HeaderMiddle from '@/components/HeaderMiddle'
export default {
  components: {
    postDetailFooter,
    comment,
    HeaderMiddle
  },
  data() {
    return {
      postId: this.$route.params.id,
      post: {},
      comments: [],
    }
  },
  methods: {

    getComments() {
      this.$axios({
        url: '/get_comments/' + this.postId,
        method: 'get'
      }).then(res => {
        console.log(res)
        this.comments = res
        this.post.comment_length = this.comments.length
      })
    }
  },
  mounted() {
    this.$axios({
      url: '/post/' + this.postId,
      method: 'get'
    }).then(res => {
      this.post = res
      this.getComments()
    })

  }
}
</script>

<style>
</style>
