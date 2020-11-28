<template>
  <div id="app">    
    <h1 class="title">Время в некоторых городах мира:</h1> 
    <TimeWorld
      v-for = "(time, keys) of timers"
      :key="keys"
      :region="time.region"
      :utc="time.utc" />    
  </div>
</template>

<script>
import TimeWorld from './components/TimeWorld.vue'

export default {
  name: 'App',
  data () {
    return {       
      timers: [
        {region: 'Всемирное координированное время (UTC): ', utc: 0},
        {region: 'Украина, Киев (+2 часа): ', utc: 120},
        {region: 'США, Кливленд (-5 часов): ', utc: -300},
        {region: 'Япония, Токио (+9 часов): ', utc: 540},
        {region: 'Великобритания , Лондон (0 часов): ', utc: 0},
        {region: 'Австралия , Сидней (+11 часов): ', utc: 660}         
      ]
    }
  },
  components: {
    TimeWorld
  }   
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;   
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.title{
  color: coral;
}
</style>
