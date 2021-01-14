<template>
<div class="flex flex-col items-center py-4">
    <NewPost />

    <Post v-for="post in posts.data" :key="post.data.id" :post="post"/>
</div>
</template>

<script>
import NewPost from '../components/NewPost'
import Post from '../components/Post'

export default {
    name: "NewsFeed",

    components: {
        NewPost,
        Post
    },

    data: () => {
        return {
            posts: null,
        }
    },

    mounted() {
        axios.defaults.headers.common['Authorization'] = 'Bearer ' + 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRmMzhhZmI3MmUwNzA0OTBlNDRkMWQwOTkzN2NkZmViOWZkZjkzNTBmZTAyZjIyNzhmZmUxNDQyYzkyMTRlMjE3NmIyODJhMTY5MDNjMzE3In0.eyJhdWQiOiIyIiwianRpIjoiZGYzOGFmYjcyZTA3MDQ5MGU0NGQxZDA5OTM3Y2RmZWI5ZmRmOTM1MGZlMDJmMjI3OGZmZTE0NDJjOTIxNGUyMTc2YjI4MmExNjkwM2MzMTciLCJpYXQiOjE2MTA2MjY0NDIsIm5iZiI6MTYxMDYyNjQ0MiwiZXhwIjoxNjQyMTYyNDQxLCJzdWIiOiIxIiwic2NvcGVzIjpbXX0.VtWIlpju6Z5HfDncT7FhVKN_Fnfe6L-wDZpv6mgPAbH-TJHfZtcFTF86qFHZy_XDUQv1GQ8UJn5d6RVlKVePAQyR7dmAPX59VmtckdCewXOWsKY2pSDXltwfAhSDtlKE65QwfXbL5cniEeetQhHqTi6WsO4_x49Z44UJfH8SvEmQ3bqpdWRUbpU6fDVI322ojk6mRph6Nv8y0cFNxVPPVof20p2f2HHEXYc6vE_QK4atFOFSXJ74M-886sMQSG9XkWfZEdZBC-I-bD41qml-9qrTI1_o4Eb6LnPEuIR89ZeZZLA5Er9UhhQHcHoCT4gQ7JIhnKt3_63fG9Rjh6VHi3QfxzFzuP601Kv0kmNCVxSYf9TZik38FP-yXIfJTuuvxFPvII_xwymG1AWjzP6c8_VVjfPmesfebwSiB4dvwol9_dsaDZY4A4HXceD13Lou__XAGielQVW05fz2d4MEI6yMx7jmmrA3pBwFRpYGIVyuScD8FUYsvzmS8NsrYqhkViSK-zgrUB4ZGi_HpxeCeqxVZ4iLmSo3sGqfHlufBJlSz-Vv4fUD_-hTL0iIxevgYa6HFUK5gOM7YCtyiLkvpdYkFoemyijXNoFn8kmdmJXLJPjKNYnC_z6q7Qm9ig4ioS4LeVGSxIMtxvnMtApkAH8T866RcpeMVSCDR6_EaAE'
        axios.get('/api/posts')
            .then(res => {
                this.posts = res.data;
            })
            .catch(error => {
                console.log('Unable to fetch posts');
            });
    }
}
</script>

<style lang="stylus" scoped>

</style>
