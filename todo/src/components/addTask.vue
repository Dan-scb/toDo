<template>
    <div>
        <input type="text" @keyup="taskChange($event)" name="newTask" placeholder="Nova tarefa?" />
        <button @click="saveTask($event)">+</button>
    </div>
    
</template>

<script>
export default {
    setup() {
        
    },
    data(){
        return {
            taskValue:''
        }
    },
    methods:{
        saveTask(){
            this.$emit('setTask', this.taskValue)
        },
        taskChange(e){
            this.taskValue = e.target.value
        }
    }
}
</script>

<style scoped>
    

    div{
        margin-top: 20px;
        width: 30vw;
        height: 4vh;
        padding: 0px;
        border: solid 1px black;
        border-radius: 4px;
       display: flex;
       

       
    }
    input{
        width: 100%;
        height: 85%;
        border: none;
        border-right: solid 1px black ;
        font-size: 1.4rem;
    }
    button{
        background-color: rgb(182, 182, 229);
        border: none;
        margin: 0px 0px;
        height: 100%;
        width: 8%;
    }
</style>