<template>
<div class="bg-white rounded shadow w-2/3 p-4">
    <div class="flex justify-between items-center">
        <div>
            <div class="w-8">
                <img :src="authUser.data.attributes.profile_image.data.attributes.path" alt="Profile image of a user" class="w-8 h-8 object-cover rounded-full">
            </div>
        </div>

        <div class="flex-1 flex mx-4">
            <input v-model="postMessage" type="text" name="body" class="w-full focus:outline-none focus:shadow-outline text-sm rounded-full text-sm pl-4 h-8 bg-gray-200" placeholder="Add a post">
            <transition name="fade">
                <button v-if="postMessage" @click="postHandler" class="bg-gray-200 ml-2 px-3 py-1 rounded-full">
                    Post
                </button>
            </transition>
        </div>
        <div>
            <button ref="postImage" class="dz-clickable flex justify-center items-center rounded-full w-10 h-10 bg-gray-200">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" class="fill-current w-5 h-5">
                    <path d="M21.8 4H2.2c-.2 0-.3.2-.3.3v15.3c0 .3.1.4.3.4h19.6c.2 0 .3-.1.3-.3V4.3c0-.1-.1-.3-.3-.3zm-1.6 13.4l-4.4-4.6c0-.1-.1-.1-.2 0l-3.1 2.7-3.9-4.8h-.1s-.1 0-.1.1L3.8 17V6h16.4v11.4zm-4.9-6.8c.9 0 1.6-.7 1.6-1.6 0-.9-.7-1.6-1.6-1.6-.9 0-1.6.7-1.6 1.6.1.9.8 1.6 1.6 1.6z" /></svg>
            </button>
        </div>
    </div>

    <div class="dropzone-previews">
        <div id="dz-template" class="hidden">
            <div class="dz-preview dz-file-preview mt-4">
                <div class="dz-details">
                    <img data-dz-thumbnail class="w-32 h-32" src="" alt="">

                    <button data-dz-remove class="text-xs">REMOVE</button>
                </div>

                <div class="dz-progress"><span class="dz-upload" data-dz-upload></span></div>
            </div>
        </div>
    </div>
</div>
</template>

<script>
import _ from 'lodash';
import { mapGetters } from 'vuex';
import Dropzone from 'dropzone';

export default {
    name: "NewPost",

    data:()=>{
        return{
            dropzone: null
        }
    },

    mounted(){
        this.dropzone = new Dropzone(this.$refs.postImage, this.settings) 
    },

    computed: {
        ...mapGetters({
            authUser: 'authUser',
        }),

        postMessage: {
            get() {
                return this.$store.getters.postMessage;
            },

            set: _.debounce(function(postMessage){
                this.$store.commit('updateMessage', postMessage)
            }, 300),
        },

        settings(){
            return{
                paramName : 'image',
                url: '/api/posts',
                acceptedFiles: 'image/*',
                clickable: '.dz-clickable',
                autoProcessQueue: false,
                maxFiles: 1,
                previewsContainer: '.dropzone-previews',
                previewTemplate: document.querySelector('#dz-template').innerHTML,
                params: {
                    'width' : 1000,
                    'height' :1000,
                },
                   headers:{
                    'X-CSRF-TOKEN': document.head.querySelector('meta[name=csrf-token]').content,
                    'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6IjczNWY3NWY2MDNkNmM0ODk1MjEwOTQ5Y2RlNGUyYzU2NjQwOTQ0MTkyNWMyOThlOWM4NWQ1YzlmMzU5ZTQyYjhmZWQxMjk2NGNkZWMxNTgwIn0.eyJhdWQiOiIyIiwianRpIjoiNzM1Zjc1ZjYwM2Q2YzQ4OTUyMTA5NDljZGU0ZTJjNTY2NDA5NDQxOTI1YzI5OGU5Yzg1ZDVjOWYzNTllNDJiOGZlZDEyOTY0Y2RlYzE1ODAiLCJpYXQiOjE2MTE1NzAyMDUsIm5iZiI6MTYxMTU3MDIwNSwiZXhwIjoxNjQzMTA2MjA1LCJzdWIiOiIxIiwic2NvcGVzIjpbXX0.nqXisW4QPcHzznp1UwUWqPPNhabKT5TL8l05JRtSiDx59BS4AeS4WsjfqzWxJdKNDYR8xDsimZi82wtTuB2HfcxORdABt0nOtF2-n4e1uI_HXLQve1R7l8iZ8LuekeBYDp_-YADJ2TqHHOi4CkD9c9vcSP0Ka10_-wMHDS8ugB2_Dfi1D2sZDoUDbYrakpZ8Pa02keTdbMlgrEDnD_BIcDJxgo6mP5-olwSibp0zSFIkNODWhQ5ix1OOm3n3nYAJFUH2EYkYG_QdrF4UU4T5hjRTWDWj1Jxjwmi-KEgQLyQqPV7iuT4sVYaAJt5Nuzn4LNDoLys2bWiLJoLC1n2sjl5oj2HunJR-x4Ci_sTb5iEHx5det0GPrc50jD3o65k4LSbVOPamdT5z54RXJ3Iri7vgZU_3b6MX3ZKnngBTqThmRsOHATBpdfkxMh9NoRgVO47h35Fml75IIlMpi4kz4WK-C-6KRFbufAzI-zSYylOm9NmLnaZSFzl_Acdc8ejcmZQT40-wPFkV7k4NoBnsB9QoFaHwnMzG0sK3OhWJIP0sWyMdC3j7vexk0TzPnZxJ2cIoJs-6OLHjp2YBlFkxpMd4_1zMpcDvZMJ1dgqoOUyON5C5jnGuyXTxyHJt6EpkP7h6y5nx8cU6IzkGbrdkOvTBASVbNvciXaSc8FX4PUQ',
                },
                sending: (file, xhr, formData) => {
                    formData.append('body', this.$store.getters.postMessage);
                },
                success: (event, res) =>{
                    this.dropzone.removeAllFiles();

                    this.$store.commit('pushPost', res)
                },
                maxfilesexceeded: file => {
                    this.dropzone.removeAllFiles();
                    this.dropzone.addFile(file);
                }
            }
        },
    },

    methods: {
        postHandler() {
            if(this.dropzone.getAcceptedFiles().length){
                this.dropzone.processQueue();
            }else{
                this.$store.dispatch('postMessage');
            }

            this.$store.commit('updateMessage', '');
        }
    }
}
</script>

<style scoped>
    .fade-enter-active, .fade-leave-active {
        transition : opacity .5s;
    }
    .fade-enter, .fade-leave-to{
        opacity: 0;
    }
</style>
