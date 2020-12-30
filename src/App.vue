<template>
  <div id="app">
    <header>
    <h1>xcrypto</h1>
    <p>_Current Bitcoin Info_</p>
    </header>  
    <div class="card" v-for="c in crypto" :key="c.id">
      <p>{{ c.name }}</p>
      <p>${{ c.price_usd}}</p>
      <p>Percent_Change(1H):{{ c.percent_change_1h }}</p>
      <p>Percent_Change(24H):{{ c.percent_change_24h }}</p>
      </div>        
    </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "App",
data() {
  return{
    crypto:null,
    loading:true,
    errored:false
  }
},  
mounted(){
  axios.get(' https://api.coinlore.net/api/ticker/?id=90 ').then(response=>{
    console.log(response);
    this.crypto = response.data
  }).catch(error=>{
    console.log(error)
    this.errored=true
  }).finally(()=>this.loading=false)
}    
};

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.card{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  padding:1em;
  border: 2px solid red;
  font-size: 1.3em;
  font-weight: 800;
}
</style>
