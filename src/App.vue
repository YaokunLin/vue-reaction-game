<template>
  <p 
   class="best-result"
   v-if="bestResult !== Number.MAX_VALUE">
   best restult: {{ bestResult }} ms
  </p>

  <h1>⚡ Reaction Game</h1>
  
  <button 
   @click="startGame" 
   :disabled="isPlaying">
      play
  </button>

  <Block 
  v-if="isPlaying" 
  :delay="delay"
  @end="updateReactionTime"
  />

  <!-- <p v-if="reactionTime"> reaction time: {{ reactionTime }} ms </p> -->

  <Results 
  v-if="reactionTime" 
  :reactionTime="reactionTime"
  />
</template>

<script>
import Block from "./components/Block.vue"
import Results from "./components/Results.vue"


export default {
  name: 'App',
  components: {
    Block,
    Results
  }, 
  data(){
    return {
      isPlaying: false,
      delay: null,
      reactionTime: null,
      bestResult : Number.MAX_VALUE,
    }
  },
  methods:{
    startGame(){
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = true
      this.reactionTime = null
    }, 
    updateReactionTime(reactionTime){
      this.reactionTime = reactionTime
      this.isPlaying = false
      this.bestResult = Math.min(this.bestResult, reactionTime)
 
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
  color: #444;
  margin-top: 60px;

}
.best-result{
  position: fixed;
  top : 0;
  right: 10px;
}
button{
  padding: 16px 32px;
  background: #0faf87;
  color: white;
  border-radius: 15px;
  margin: 10px;
  cursor: pointer;
  border: none;
}

button:hover{

  background: black;
  color: white;
  content:"++"
 
}

button[disabled]{
  cursor: not-allowed;
  color: white;
  background:grey
}
</style>
