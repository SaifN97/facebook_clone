<template>
<div class="flex flex-col items-center py-4">
    <NewPost />
    <p v-if="loading">Loading posts</p>
    <Post v-else v-for="post in posts.data" :key="post.data.id" :post="post"/>
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
            loading: true
        }
    },

    mounted() {
        axios.defaults.headers.common['Authorization'] = 'Bearer ' + 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6IjY0Yzk2ODQ2MjY5ZTQ5ZDJkMTgzNzZhYzZjMGU4ZTU5NzBlNDAxMzhlYTcyM2M5ZDBkNTZkMjdkNTFlMjkxODI0ODUyODIyNjAyNjlkYTdiIn0.eyJhdWQiOiIyIiwianRpIjoiNjRjOTY4NDYyNjllNDlkMmQxODM3NmFjNmMwZThlNTk3MGU0MDEzOGVhNzIzYzlkMGQ1NmQyN2Q1MWUyOTE4MjQ4NTI4MjI2MDI2OWRhN2IiLCJpYXQiOjE2MTA3MTYxODQsIm5iZiI6MTYxMDcxNjE4NCwiZXhwIjoxNjQyMjUyMTg0LCJzdWIiOiIxIiwic2NvcGVzIjpbXX0.d-BBUp789US5P2pt_Ce48LjPqlVl0wPB-AaG2Pgb8PgQpYp7JF-_fciD2LRyDQLKTn9__BR8tx4cA_eMU6wAIWqjvQBFWD-oUb2gU7hAPf4L67dqF1mdbiA5z9yhTOzK1RWZ_FgKbhtr4ZzCEIEPZ4elDKU269A_OERj0Xvilf_cnZ2-DiMJ9MQTTClFazLg5kbwH01e_mRDacftngD_OIM_2Fr_laEMO5cFnZwXY9gPQJ-4lsrvpK4sJn0d-t9rQRKyAWW1v98sgIw_AoqD_r0YApfeRUH95Nq1oVJaF0RDwBzKo204cw_YPHdpIViL64dtvlgoBafjWi0GhTRDZtg84Gfaj0iJyrw4Ak45yKtKRUPUOMegd_prYLOToagZy3jRSFcqFQ_CVOfEe6UhiEmSmgZGxGgG_R_2SxasyS9oFoVFqG2g5rD7g4AB9q6H0ule5jcdYMxSvQ9f2JognY5WqWIZfA7sYuBS41DPr_D1IVrt83i2ujAFnewHbQLO9XXk1xpy2A3aTUuiFwWk9RNuoqg7mW2Ly-v-Xf7HHpPn8-b3AetMAG3-_D0x_EP0tBjNivVjpYRftrlXKLQh0R6ubE0XFVt4I7spE6E0YZovbSBqg-WWNW20iFLOjrnFmepvTelCrUF2vg6EpS4SQb4GQIRKdktp1Dv4zW43ehk'
        axios.get('/api/posts')
            .then(res => {
                this.posts = res.data;
                this.loading = false;
            })
            .catch(error => {
                console.log('Unable to fetch posts');
                this.loading = false;
            });
    }
}
</script>

<style lang="stylus" scoped>

</style>
