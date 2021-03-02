

<template>
    <div id="login">
        <h1>Login</h1>
        <input type="text" 
        class="username"
        name="username" v-model="input.username" placeholder="Username" />
        <input type="password" 
        class="password"
        name="password" v-model="input.password" placeholder="Password" />
        <button type="button"
        class="button" v-on:click="login()">Login</button>
    </div>
</template>

<script>
import axios from 'axios';
    export default {
        name: 'Login',
        data() {
            return {
                input: {
                    username: "",
                    password: ""
                }
            }
        },
        methods: {
            login() {
                if(this.input.username != "" && this.input.password != "") {
                    const dataForPostRequest = { "username": this.input.username , "password":this.input.password};
                    axios.post("https://aodapi.eralpsoftware.net/login/apply", dataForPostRequest)
                    .then((response) => {
                        console.log(response)
                        this.$emit("authenticated", true)
                        this.$router.replace({ name: "secure" })
                    }
                    
                    ).catch(() => console.log("Yanlış şifre veya kullanıcı adı."));
                }

                    
                    


            }     
        }
    }
</script>

<style scoped>
    #login {
        width: 500px;
        border: 1px solid #CCCCCC;
        background-color: #FFFFFF;
        margin: auto;
        margin-top: 200px;
        padding: 20px;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
    .username {
        margin-bottom: 10px;
    }
    .password {
        margin-bottom: 10px;
    }
    .button {
        background-color: blue;
        border:none;
        padding:10px 50px;
    }
</style>