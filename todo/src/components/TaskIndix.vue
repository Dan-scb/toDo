<template>
    <div>
        <h2>Tarefas</h2>
        <div class="progressBar">
            
            <div class="ratingBar" :style="{'width':concBar}">
               <strong>{{concBar}}</strong> 
            </div>
            
            </div>
    </div>
</template>

<script>
export default {
    props:{concBar: String},
    
    
}
</script>

<style scoped>
    .progressBar{
        width: 80vw;
        height: 2vh;
        border: solid 2px black;
        border-radius: 4px;
        
    }
    .ratingBar{
        width: 0%;
        height: 100%;
        color: rgb(190, 92, 92);
        background-color: rgb(68, 235, 68);   
    }
    .ratingBar > strong{
        display: block;
        position: absolute;
        left: 50%;
    }

</style>