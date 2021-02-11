<template>
<div>
    <img 
    :class="classes" 
    :src="userImage.data.attributes.path" 
    ref="userImage"
    :alt="alt">

</div>
</template>

<script>
import Dropzone from 'dropzone';
import { mapGetters } from 'vuex';

export default {
    name:"UploadableImage",

    props:[
        'userImage',
      'imageWidth',  
      'imageHeight',  
      'location',  
      'classes',  
      'alt',  
    ],

    data: () => {
        return {
            dropzone:null,
        };
    },

    mounted(){ 
        if (this.authUser.data.user_id.toString() === this.$route.params.userId) {
        this.dropzone = new Dropzone(this.$refs.userImage, this.settings);
        }
    },

    computed:{
        ...mapGetters({
            authUser:'authUser',
        }),
        settings(){
            return{
                paramName: 'image',
                url: '/api/user-images',
                acceptedFiles: 'image/*',
                params: {
                    'width': this.imageWidth,
                    'height': this.imageHeight,
                    'location': this.location,
                },
                headers:{
                    'X-CSRF-TOKEN': document.head.querySelector('meta[name=csrf-token]').content,
                    'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6IjczNWY3NWY2MDNkNmM0ODk1MjEwOTQ5Y2RlNGUyYzU2NjQwOTQ0MTkyNWMyOThlOWM4NWQ1YzlmMzU5ZTQyYjhmZWQxMjk2NGNkZWMxNTgwIn0.eyJhdWQiOiIyIiwianRpIjoiNzM1Zjc1ZjYwM2Q2YzQ4OTUyMTA5NDljZGU0ZTJjNTY2NDA5NDQxOTI1YzI5OGU5Yzg1ZDVjOWYzNTllNDJiOGZlZDEyOTY0Y2RlYzE1ODAiLCJpYXQiOjE2MTE1NzAyMDUsIm5iZiI6MTYxMTU3MDIwNSwiZXhwIjoxNjQzMTA2MjA1LCJzdWIiOiIxIiwic2NvcGVzIjpbXX0.nqXisW4QPcHzznp1UwUWqPPNhabKT5TL8l05JRtSiDx59BS4AeS4WsjfqzWxJdKNDYR8xDsimZi82wtTuB2HfcxORdABt0nOtF2-n4e1uI_HXLQve1R7l8iZ8LuekeBYDp_-YADJ2TqHHOi4CkD9c9vcSP0Ka10_-wMHDS8ugB2_Dfi1D2sZDoUDbYrakpZ8Pa02keTdbMlgrEDnD_BIcDJxgo6mP5-olwSibp0zSFIkNODWhQ5ix1OOm3n3nYAJFUH2EYkYG_QdrF4UU4T5hjRTWDWj1Jxjwmi-KEgQLyQqPV7iuT4sVYaAJt5Nuzn4LNDoLys2bWiLJoLC1n2sjl5oj2HunJR-x4Ci_sTb5iEHx5det0GPrc50jD3o65k4LSbVOPamdT5z54RXJ3Iri7vgZU_3b6MX3ZKnngBTqThmRsOHATBpdfkxMh9NoRgVO47h35Fml75IIlMpi4kz4WK-C-6KRFbufAzI-zSYylOm9NmLnaZSFzl_Acdc8ejcmZQT40-wPFkV7k4NoBnsB9QoFaHwnMzG0sK3OhWJIP0sWyMdC3j7vexk0TzPnZxJ2cIoJs-6OLHjp2YBlFkxpMd4_1zMpcDvZMJ1dgqoOUyON5C5jnGuyXTxyHJt6EpkP7h6y5nx8cU6IzkGbrdkOvTBASVbNvciXaSc8FX4PUQ',
                },
                success:(e, res) => {
                    this.$store.dispatch('fetchAuthUser');
                    this.$store.dispatch('fetchUser', this.$route.params.userId );
                    this.$store.dispatch('fetchUserPosts', this.$route.params.userId );
                } 
            };
        },
    }
}
</script>

<style scoped>

</style>
