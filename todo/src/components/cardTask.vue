<template>
    <div class="card" :style="{'background-color':setState}">
        <button @click="deleteTask">x</button>
        <span @click="state">
        <slot />
        </span>
    </div>
        
    
</template>

<script>
export default {
    props:{
        clear: Boolean,
        conclude: Boolean
        },
    setup() {
        
    },
    data(){
        return{
            pendence: true,
            setState: 'rgb(95, 83, 83)',
            concludes:  true

        }
    },
    methods:{
        state(){
         this.pendence = this.pendence ? false : true
         this.setState =  this.pendence ? 'rgb(95, 83, 83)' : 'rgb(133, 153, 77)'
         if(this.pendence){
             this.$emit('progress', 'fail')
         }else{
             this.$emit('progress','ok')
         }
         
        },
        deleteTask(){
        this.state()    
        this.$emit('delT','')
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
    .card{
        background-color:rgb(95, 83, 82);
       
        width: 25vw;
        height: 15vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-evenly;
        color: #fff;
        font-size: 1.4rem;
        border: inset 3px black;
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