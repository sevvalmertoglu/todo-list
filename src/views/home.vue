<template>
    <div id="home">
        <h1>Home Page</h1>
       
         
        <h1>Add tasks</h1>  
        <input type="text" 
        class="task"
        name="task" v-model="input.task" placeholder="write-task" />
        <input type="text" 
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
        props: ['ourToken'],
        data() {
            return {
                input: {
                    task: "",
                    data: ""  
                }, 
            
        
            };  
        },

        methods: {
            addTasks() {
                if(this.input.task != "" && this.input.date != "") { 
                    const dataForPostRequest = { "tasks": this.input.task , "date":this.input.date}; 
                    axios.post("https://aodapi.eralpsoftware.net/todo", dataForPostRequest, {
                        headers:{
                            Authorization: 'Bearer ' + this.props}
                    }) 
                    .then((response) => {
                        console.log(response)
                        
                        this.$emit("authenticated", true)
                        this.$router.replace({ name: "home" })
                    }
                    
                    ).catch(() => console.log("error"));     
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
        padding: 20px;
        display: flex;
        flex-direction: column;
        align-items: upper right corner;
        justify-content: upper right corner;
    }
    .wrtask {
        margin-bottom: 20px; 
        border-radius: 11px;
    }
    .date { 
        margin-bottom: 20px;
        border-radius: 11px;
    }
    .button {
        background-color: red;
        border:none;
        padding:10px 50px;
    }

</style>
