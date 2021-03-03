<template>
    <div id="home">
        <h1>Home Page</h1>
        <p>
            This is a Home
        </p>
         
        <h1>tasks</h1> 
        <input type="text" 
        class="task"
        name="task" v-model="input.task" placeholder="write-task" />
        <input type="password" 
        class="date" 
        name="date" v-model="input.date" placeholder="date" />
        <button type="button"
        class="button" v-on:click="addTasks()">home</button>
    </div>
</template>

<script> 
import axios from 'axios'; 
    export default {
        name: 'Home',
        data() {
            return {
                input: {
                    task: "",
                    data: "" 
                }
            };  
        },

        methods: {
            addTasks() {
                if(this.input.task != "" && this.input.date != "") { 
                    const dataForPostRequest = { "tasks": this.input.task , "date":this.input.date};
                    axios.post("https://aodapi.eralpsoftware.net/", dataForPostRequest)
                    .then((response) => {
                        console.log(response)
                        this.$emit("authenticated", true)
                        this.$router.replace({ name: "home" })
                    }
                    
                    ).catch(() => console.log("unfinished task"));
                }
            }

                    
                    


         }      
        
    }
</script>

<style scoped>
    #home {
        background-color: #FFFFFF;
        border: 1px solid #CCCCCC;
        padding: 20px;
        margin-top: 10px;
    }
    .wrtask {
        margin-bottom: 10px; 
    }
    .date { 
        margin-bottom: 10px;
    }
    .button {
        background-color: red;
        border:none;
        padding:10px 50px;
    }

</style>
