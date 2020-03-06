<template>
    <div>
        <homeHeader></homeHeader>
        <div>
          <post v-for="(item,index) in posts" :key="index" :post="item"></post>
        </div>

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
            posts: [
        {
          'id':11,
          'type':2,
          'title':'而停止关注这个用户，而停止关注这个用户，而停止关注这个用户，而停止关注这个用户，可以这样做',
          'comment_length':2,
          'user':{
            'nickname':'zhangsan'
          },
          'cover':[{'url':'https://upload-images.jianshu.io/upload_images/13746487-4b74de284d91f490.png?imageMogr2/auto-orient/strip|imageView2/2/w/514/format/webp'}
          ,{'url':'https://upload-images.jianshu.io/upload_images/13746487-4b74de284d91f490.png?imageMogr2/auto-orient/strip|imageView2/2/w/514/format/webp'}
          ,{'url':'https://upload-images.jianshu.io/upload_images/13746487-4b74de284d91f490.png?imageMogr2/auto-orient/strip|imageView2/2/w/514/format/webp'}]
        },
        {
          'id':12,
          'type':1,
          'title':'而停止关注这个用户，而停止关注这个用户，而停止关注这个用户，而停止关注这个用户，可以这样做',
          'comment_length':2,
          'user':{
            'nickname':'zhangsan'
          },
          'cover':[{'url':'https://upload-images.jianshu.io/upload_images/13746487-4b74de284d91f490.png?imageMogr2/auto-orient/strip|imageView2/2/w/514/format/webp'}
            ,{'url':'https://upload-images.jianshu.io/upload_images/13746487-4b74de284d91f490.png?imageMogr2/auto-orient/strip|imageView2/2/w/514/format/webp'}]
        },
        {
          'id':13,
          'type':1,
          'title':'而停止关注这个用户，而停止关注这个用户，而停止关注这个用户，而停止关注这个用户，可以这样做',
          'comment_length':2,
          'user':{
            'nickname':'zhangsan'
          },
           'cover':[{'url':'https://upload-images.jianshu.io/upload_images/13746487-4b74de284d91f490.png?imageMogr2/auto-orient/strip|imageView2/2/w/514/format/webp'}
          ,{'url':'https://upload-images.jianshu.io/upload_images/13746487-4b74de284d91f490.png?imageMogr2/auto-orient/strip|imageView2/2/w/514/format/webp'}
          ,{'url':'https://upload-images.jianshu.io/upload_images/13746487-4b74de284d91f490.png?imageMogr2/auto-orient/strip|imageView2/2/w/514/format/webp'}]
        }
    ]
          }
        }
    }
</script>

<style scoped>

</style>
