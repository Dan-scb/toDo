<template>
  <div class="el" :key="componentKey">
    <img alt="Vue logo" src="./assets/logo.png">
  <task-indix :concBar="concBar" />
  <add-task @setTask="run"  />

  <div class="logs">
    <div class="log"  v-for="(c, index) in tasks" :key="index" >
        <card-task  @progress="conclusion" @delT="delTask($event, c)"> <p> {{c}} </p> </card-task>
    </div>
  </div>
  </div>
  
</template>

<script>

import TaskIndix from './components/TaskIndix.vue'
import addTask from './components/addTask.vue'
import cardTask from './components/cardTask.vue'
export default {
  name: 'App',
  data(){
    return{
      tasks:[],
      concludeTasks:0,
      percentConc: 0,
      concBar: '0%',
      concludes: true,
      componentKey:0
      
    }
  },
  components: {
    TaskIndix,
    addTask,
    cardTask
  },
  methods:{
    run(e){
      this.tasks.push(e)
      this.concludeTasks++
      this.conclusion('')
    },
    conclusion(e){
      if(e == 'ok'){
       this.concludeTasks++
       console.log(this.concludeTasks)
     let porcent = this.concludeTasks / this.tasks.length
      this.percentConc = 100 * porcent
      this.concBar = `${this.percentConc}%`

      }else if(e == 'del'){  
      let porcent = this.concludeTasks / this.tasks.length
      this.percentConc = 100 * porcent
      this.concBar = this.percentConc != Number ? '0%' : `${this.percentConc}%`
      }
      else{
      this.concludeTasks = this.tasks.length == 0 ?  0 :this.concludeTasks--
        console.log(this.concludeTasks)
        let porcent = this.concludeTasks <= 0 ? this.concludeTasks = 0 : this.concludeTasks  / this.tasks.length
      this.percentConc = 100 * porcent
      this.concBar = `${this.percentConc}%`
      }
    },
    delTask(event,t){
      
      if(event){
       this.tasks = this.tasks.filter(el => el != t)
       this.componentKey +=1
       this.conclusion('del')
      }else{
    this.concludeTasks--  
     this.tasks = this.tasks.filter(el => el != t)
     this.componentKey +=1
     this.conclusion('f')
      }
      
    }
    
  }
}
</script>

<style>
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
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
  }
</style>
