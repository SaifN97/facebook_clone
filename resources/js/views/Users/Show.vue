<template>
    <div>
        <div class="w-100 h-64 overflow-hidden">
        <img class="object-cover w-full" src="https://upload.wikimedia.org/wikipedia/commons/6/6e/Monasterio_Khor_Virap%2C_Armenia%2C_2016-10-01%2C_DD_25.jpg" alt="user background image">
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Show',

        data: () => {
            return {
                user: null,
                loading:true
            }
        },

        mounted() {
        axios.defaults.headers.common['Authorization'] = 'Bearer ' + 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImEyYTA1NmE2MTIwOTNhZjg4ZTFlNTkwNWExMmJjMjM1OTQwMmZmNTU2OGQyYTliYTY5M2Q0NGVjZjU4ZWE2ZDRkYzRmOTYzMTMxNWJlZGUwIn0.eyJhdWQiOiIyIiwianRpIjoiYTJhMDU2YTYxMjA5M2FmODhlMWU1OTA1YTEyYmMyMzU5NDAyZmY1NTY4ZDJhOWJhNjkzZDQ0ZWNmNThlYTZkNGRjNGY5NjMxMzE1YmVkZTAiLCJpYXQiOjE2MTA4ODE2OTgsIm5iZiI6MTYxMDg4MTY5OCwiZXhwIjoxNjQyNDE3Njk4LCJzdWIiOiIxIiwic2NvcGVzIjpbXX0.C5pinY7sIMWqpXTImfPHHdCHU22ppgK_D2T7-k1YHUWgAap6bhS_M2cjF3dc20FHEyTs4Bdypl_67Ez2bZqdDBzJl2tPFtJYaqxsmz3kraMmQTuzURw3rmUKrvO1WCh-TiNQOlgA5wUPgQ_PVGhGzxcTFQsIQ5ceIBFNVyhScJUmjvPkoNojXlbn9K-8LeqLCAkuzc-4UKKOksE_H-NSkwR9tZ-w62wjV4PIBhzX2b4bP5KImvu_eNzT4arZkh-ekNdUevBgXlxWh6uSd5XNTLx7tlGfYkwENn0TGZ5j4VXaRhHRl0SNHG2jgKoTCc9ZEdBqnVunLqSk4npvFvMENEioHV2RNpQhqPWqGtDLlAIgSqVMjen6Tsu2hCAwaktMUzzWzO7GYphvliVa2egwG_tMHSnTp2o_ueFlDkj1CyOhHM1YfklNf_FTWifOotnJS9CPXHQORc-bw6w19ciM2AvTqyGc8UT-aoSFYqtIIt8AyFIlE99cogmZM42ihhGQ9AVebcj_jtEbnP4TXRSnhpH85tc08oTcDUXHGwdg9HMSUWMiybVPURb2uUPMoAIw60tjn4F0edhbm7EuUzb-Ic7QvGbWyTBpMrs4KyG01vQNHQFh_0XqWE3UsapuHvBSQ5zryUDWkhDh2eoI7Pdxxm2HJzbvsolbqDVv7U4AH7k'

            axios.get('/api/users/' + this.$route.params.userId)
            .then(res => {
                this.user = res.data;
            })
            .catch(err => {
                console.error('Unable to fetch users from the server.'); 
            })
            .finally(()=>{
                this.loading = false;
            })
        }
    }
</script>

<style scoped>

</style>