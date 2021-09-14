<template>
      <div class="progress">
      <div class="progress-bar bg-info" role="progressbar" :style="{width:length*10+'%'}" aria-valuenow="50" aria-valuemin="0" aria-valuemax="100">
        {{length}}/10
      </div>
    </div>
</template>


<script>
import {eventBus} from "../main"
export default {
    data(){
        return{
            length:0
        }
    },
    created(){
        eventBus.$on("productAdded",(data)=>{
            this.length=data.length
          
            
        })
    }
}
</script>