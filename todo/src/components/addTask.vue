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
        margin-top: 40px;
        width: 30vw;
        height: 4vh;
        padding: 0px;
        border: solid 3px rgb(170, 157, 157);
        border-radius: 4px;
       display: flex;      

    }
    input{
        width: 100%;
        height: 100%;
        border: none;
        border-right: solid 1px black ;
        background-color: rgb(232, 236, 241);
        font-size: 1.4rem;
    }
    button{
        background-color: rgb(73, 73, 83);
        font-size: 1.4rem;
        border: none;
        margin: 0px 0px;
        height: 104%;
        width: 6%;
    }
    input:focus{
        outline: none;
    }
</style>