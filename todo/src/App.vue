<template>
  <div class="el" :key="componentKey">
    <img alt="Vue logo" src="./assets/logo.png">
  <task-indix :concBar="concBar"/>
  <add-task @setTask="run"  />
  <warning-task v-if="caution == true" />
  <div class="logs">
    <div class="log"  v-for="(c, index) in tasks" :key="index"  >
        <card-task  @progress="conclusion($event,c)" :conclude="true"  @delT="delTask(c, index)"> <p> {{c}} </p> </card-task>
    </div>
  </div>
  </div>
  
</template>

<script>

import TaskIndix from './components/TaskIndix.vue'
import addTask from './components/addTask.vue'
import cardTask from './components/cardTask.vue'
import WarningTask from './components/WarningTask.vue'
export default {
  name: 'App',
  data(){
    return{
      tasks:[],
      concludeTasks:[],
      percentConc: 0,
      concBar: '0%',
      concludes: true,
      caution: false
      
    }
  },
  components: {
    TaskIndix,
    addTask,
    cardTask,
    WarningTask
  },
  methods:{
    run(e){
      let element = this.tasks.filter(element => element == e)
      if(element.length > 0){
        this.caution = true
        setTimeout(() => this.caution = false, 5000)
      }else{
      this.tasks.push(e)
      this.conclusion('', undefined)
      }
      
    },
     conclusion(e, c){

      if(e == 'ok'){
      this.concludeTasks.push(c)
      let porcent = this.concludeTasks.length / this.tasks.length
      this.percentConc = parseInt(100 * porcent)
      this.concBar = `${this.percentConc}%`
      

      }else{  
      this.concludeTasks = this.concludeTasks.filter(element => element != c) 
      let porcent = this.concludeTasks.length / this.tasks.length
      this.percentConc = parseInt(100 * porcent)
      this.concBar =`${this.percentConc}%`
      
      }
      
    },
    delTask(c){
      this.tasks = this.tasks.filter(element => element != c)
      this.concludeTasks = this.concludeTasks.filter(element => element != c)

      if(this.tasks.length == 0){
        this.concBar =`${0}%`
      }else{
        this.conclusion('fa', NaN)
        
             
      }
      
    },
    
  }
  
}
</script>

<style >
body{
  background-image: linear-gradient(to right, #2c3e50, #54718f)
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}

  .el{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .logs{
    width: 80vw;
    margin-top: 50px;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    gap: 25px;
  }
</style>
