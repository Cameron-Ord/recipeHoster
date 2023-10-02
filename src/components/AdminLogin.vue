
<template>
    <span class="AdminLogin">
        <div class="usernameInput">
            <input placeholder="username" ref="username" type="text">
        </div>
        <div class="passwordInput">
            <input placeholder="password" ref="password" type="password" @keyup.enter="admin_login(this.$refs.username, this.$refs.password)">
        </div>
    </span>
</template>

<script>
import Cookies from 'vue-cookies';
import axios from 'axios'
    export default {
        components:{

        },

        data() {
            return {
                
            }
        },

        methods:{
            admin_login(username,password){
                console.log(import.meta.env.VITE_APP_BASE_DOMAIN)
                axios({
                    url: `${import.meta.env.VITE_APP_BASE_DOMAIN}/api/adminLogin`,
                    method:'POST',
                    data:{
                        username: username.value,
                        password: password.value
                    }
                }).then((response)=>{
                    Cookies.set('adminInfo', response['data'][0])
                    const info=Cookies.get('adminInfo');
                    console.log(info['admin_id'],info['session_token'])
                }).catch((error)=>{
                    error;
                })
            }
        },
        computed:{

        },
        created(){

        },
        mounted(){

        },
        beforeMount(){

        },
        beforeUpdate(){

        },
        updated(){

        },
        beforeUnmount(){

        },
        unmounted(){

        }

    }
</script>

<style lang="scss" scoped>
.AdminLogin{
    display: grid;
    align-items: center;
    justify-items: center;
    grid-auto-flow: row;
    row-gap: 25px;

    >.passwordInput{
        display: grid;
        >input{
            padding: 10px;
        }
    }
    >.usernameInput{
        display: grid;
        >input{
            padding: 10px;
        }
    }
}
</style>


