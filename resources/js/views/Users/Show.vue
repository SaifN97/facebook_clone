<template>
    <div class="flex flex-col items-center" v-if="status.user === 'success' && user">
        <div class="relative mb-8">
            <div class="w-100 h-64 overflow-hidden z-10">
                <UploadableImage image-width="1500" image-height="300" location="cover"/>
            </div>

            <div class="absolute flex items-center bottom-0 left-0 -mb-8 ml-12 z-20">
                <img src="https://hips.hearstapps.com/hmg-prod.s3.amazonaws.com/images/gettyimages-1981871a-1560281723.jpg?crop=0.586xw:0.878xh;0.243xw,0.122xh&resize=640:*"
                 alt="user profile image" class="object-cover w-32 h-32 border-4 border-gray-200 rounded-full shadow-lg">
                <p class="text-2xl text-gray-100 ml-4">{{ user.data.attributes.name }}</p>
            </div>

            <div class="absolute flex items-center bottom-0 right-0 mb-4 mr-12 z-20">
                <button v-if="friendButtonText && friendButtonText !== 'Accept'" class="py-1 px-3 bg-gray-400 rounded"
                @click="$store.dispatch('sendFriendRequest', $route.params.userId)">
                    {{ friendButtonText }}
                </button>
                
                <button v-if="friendButtonText && friendButtonText === 'Accept'" class=" mr-1 py-1 px-3 bg-blue-500 rounded"
                @click="$store.dispatch('acceptFriendRequest', $route.params.userId)">
                    Accept
                </button>

                <button v-if="friendButtonText && friendButtonText === 'Accept'" class="py-1 px-3 bg-gray-400 rounded"
                @click="$store.dispatch('ignoreFriendRequest', $route.params.userId)">
                    Ignore
                </button>
            </div>
        </div>
        
            <div v-if="status.posts === 'loading'">Loading posts</div>
            <div v-else-if="posts.length < 1">Nothing posted yet. Get Started.</div>
            <Post v-else v-for="(post, postKey) in posts.data" :key="postKey" :post="post"/>

    </div>
</template>

<script>
import Post from '../../components/Post.vue';
import UploadableImage from '../../components/UploadableImage'
import {mapGetters} from 'vuex'; 

    export default {
  components: { Post, UploadableImage },
        name: 'Show',

        mounted() {
        axios.defaults.headers.common['Authorization'] = 'Bearer ' + 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6IjczNWY3NWY2MDNkNmM0ODk1MjEwOTQ5Y2RlNGUyYzU2NjQwOTQ0MTkyNWMyOThlOWM4NWQ1YzlmMzU5ZTQyYjhmZWQxMjk2NGNkZWMxNTgwIn0.eyJhdWQiOiIyIiwianRpIjoiNzM1Zjc1ZjYwM2Q2YzQ4OTUyMTA5NDljZGU0ZTJjNTY2NDA5NDQxOTI1YzI5OGU5Yzg1ZDVjOWYzNTllNDJiOGZlZDEyOTY0Y2RlYzE1ODAiLCJpYXQiOjE2MTE1NzAyMDUsIm5iZiI6MTYxMTU3MDIwNSwiZXhwIjoxNjQzMTA2MjA1LCJzdWIiOiIxIiwic2NvcGVzIjpbXX0.nqXisW4QPcHzznp1UwUWqPPNhabKT5TL8l05JRtSiDx59BS4AeS4WsjfqzWxJdKNDYR8xDsimZi82wtTuB2HfcxORdABt0nOtF2-n4e1uI_HXLQve1R7l8iZ8LuekeBYDp_-YADJ2TqHHOi4CkD9c9vcSP0Ka10_-wMHDS8ugB2_Dfi1D2sZDoUDbYrakpZ8Pa02keTdbMlgrEDnD_BIcDJxgo6mP5-olwSibp0zSFIkNODWhQ5ix1OOm3n3nYAJFUH2EYkYG_QdrF4UU4T5hjRTWDWj1Jxjwmi-KEgQLyQqPV7iuT4sVYaAJt5Nuzn4LNDoLys2bWiLJoLC1n2sjl5oj2HunJR-x4Ci_sTb5iEHx5det0GPrc50jD3o65k4LSbVOPamdT5z54RXJ3Iri7vgZU_3b6MX3ZKnngBTqThmRsOHATBpdfkxMh9NoRgVO47h35Fml75IIlMpi4kz4WK-C-6KRFbufAzI-zSYylOm9NmLnaZSFzl_Acdc8ejcmZQT40-wPFkV7k4NoBnsB9QoFaHwnMzG0sK3OhWJIP0sWyMdC3j7vexk0TzPnZxJ2cIoJs-6OLHjp2YBlFkxpMd4_1zMpcDvZMJ1dgqoOUyON5C5jnGuyXTxyHJt6EpkP7h6y5nx8cU6IzkGbrdkOvTBASVbNvciXaSc8FX4PUQ'

           this.$store.dispatch('fetchUser', this.$route.params.userId );
           this.$store.dispatch('fetchUserPosts', this.$route.params.userId );
        },

        computed:{
            ...mapGetters({
                user: 'user',
                posts: 'posts',
                status: 'status',
                friendButtonText: 'friendButtonText',
            })
        }
    }
</script>

<style scoped>

</style>