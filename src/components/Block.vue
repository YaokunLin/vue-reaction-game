<template>
  <div 
    class="block" 
    v-if="showBlock" 
    @click="stopTimer"
    :style="{
      marginLeft: marginLeft,
      marginTop: marginTop,
      }"
    >
    click me
  </div>
  
</template>

<script>
export default {
  props:['delay'],
  data(){
    return {
      showBlock: false,
      reactionTime: 0, 
      timer: null,
      marginLeft: null,
      marginTop: null,
    }
  },
  mounted(){
    
    setTimeout(
      () => {
        this.marginLeft = ((Math.random() * 0.8) * 100).toString() + "%" // [0%, 80%] 
        this.marginTop = ((Math.random() * 0.3 - 0.1) * 100).toString() + "%" // [-10%, 20%] 
        this.showBlock = true
        this.startTimer()
      }, 
      this.delay
      )
  }, 
  methods:{
    startTimer(){
      this.timer = setInterval(
        () => this.reactionTime += 10,
        10)
    }, 
    stopTimer(){
      clearInterval(this.timer)
      this.$emit('end', this.reactionTime)
    }
  }

}
</script>

<style>
  .block{
    width:400px;
    border-radius: 20px;
    background-color: #0faf87;
    color:white;
    padding: 100px 0;
    cursor: pointer;

  }
  .block:hover{
   
    background-color: black;
  

  }
</style>