<template>
  <div class="wrap">    
    <span>{{ region }}</span> 
    <span>{{ strDate }}</span>     
    <button v-on:click="handleClick" class="btn">{{ marker ? 'STOP' : 'START' }}</button>       
  </div>
</template>

<script>
export default {
  name: 'TimeWorld',
  props: ['region', 'utc'],
  created(){     
    this.tick();
  },
  destroyed(){
    clearTimeout(this.time);
  },
  data(){
    return {
      strDate: this.dateUtc(),
      time: '',
      strBtn: 'Stop',
      marker: true      
    }
  },
  methods:{
    dateUtc(){   
      let date = new Date();
      let y = date.getUTCFullYear();
      let m = date.getUTCMonth();
      let d = date.getUTCDate();
      let h = date.getUTCHours();      
      let mn = date.getUTCMinutes() + Number(this.utc);      
      let s = date.getUTCSeconds();
      let newDate = new Date(y, m, d, h , mn, s);
      this.strDate = newDate.toLocaleString();           
    }, 
    tick(){
      this.time = setInterval(()=> {
        this.dateUtc();          
      },1000);
    }, 
    handleClick(e){
      this.marker = !this.marker;
      if (e.target.innerHTML === 'STOP'){
        clearTimeout(this.time);
      }
      else{
        this.time = setInterval(()=> {
          this.dateUtc();          
        },1000);
      }     
    }
  }   
}
</script>
 
<style scoped>
.wrap{    
  border: 1px solid ;
  border-radius: 5px;
  padding: 20px;
  width: 80%;
  max-width: 550px;
  margin: 0 auto 20px auto;
  box-shadow:
  0 1px 4px rgba(0, 0, 0, .3),
  -23px 0 20px -23px rgba(0, 0, 0, .8),
  23px 0 20px -23px rgba(0, 0, 0, .8),
  0 0 40px rgba(0, 0, 0, .1) inset;
}
.wrap:hover,
.btn:hover {
  cursor: pointer;
  font-weight: bold;
} 
.btn{
  display: block;
  margin: 10px auto 0 auto;
} 
</style>