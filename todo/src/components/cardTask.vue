<template>
    <div  :style="{'background-color':setState}" v-if="concludes">
        <button @click="deleteTask">x</button>
        <span @click="state">
        <slot />
        </span>
    </div>
    
</template>

<script>
export default {
    props:{clear: Boolean},
    setup() {
        
    },
    data(){
        return{
            pendence: true,
            setState: 'rgb(224, 82, 82)',
            concludes:  true

        }
    },
    methods:{
        state(){
         this.pendence = this.pendence ? false : true
         this.setState =  this.pendence ? 'rgb(224, 82, 82)' : 'green'
         if(this.pendence){
             this.$emit('progress', 'fail')
         }else{
             this.$emit('progress','ok')
         }
         
        },
        deleteTask(){
        this.$emit('delT', this.pendence)
        this.concludes = false
        }
    },
    computed:{
        clearSpace(){
            return this.deleteTask()
        }
    }
}

</script>
<style scoped>
    div{
        background-color:rgb(224, 82, 82);
        margin: 5px;
        width: 25vw;
        height: 15vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-evenly;
        color: #fff;
    }
    button{
        align-self: flex-end;
        margin-right: 16px;
        
        border-radius: 10px;
        background-color: coral;
        border: none;
        box-shadow: 2px 2px 7px 2px black;
    }
</style>