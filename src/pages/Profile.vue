<template>
    <div>
      <cellBar @click="$router.push('/myFollow')" label="我的关注" desc="关注的用户"></cellBar>
      <cellBar @click="$router.push('/myComments')" desc="我的跟帖" label="跟帖/回复"></cellBar>
      <cellBar @click="$router.push('/myCollections')" desc="我的收藏" label="文章/视频"></cellBar>
      <cellBar @click="$router.push('/tabManager')" label="栏目管理"></cellBar>
      <cellBar @click="$router.push('/editProfile')" label="设置"></cellBar>
      <cellBar @click="$router.replace('/login')" label="退出"></cellBar>
    </div>
</template>

<script>
    import cellBar from '@/components/cellBar'
    export default {
        name: "Profile",
        components:{
          cellBar
        }
    }
</script>

<style scoped>

</style>
