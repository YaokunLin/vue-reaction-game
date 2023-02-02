<template>
  <p > reaction time: {{ reactionTime }} ms  {{ rank }}</p>
 
</template>

<script>

export default {
  props:['reactionTime'],
  data(){
    return {
      rank: null
    }
  },

   mounted(){

    if(this.reactionTime === null){
      return
    }

    if (this.reactionTime < 500){
      this.rank = "👍👍"
    } else if(this.reactionTime < 750){
      this.rank = "👍" 
    } else{
      this.rank = "👎"
    }

  } 

}

</script>

<style>

</style>