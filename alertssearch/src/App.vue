<template>
  <div id="app">     
    <alert-component :alert="alert"></alert-component>   
  </div>
</template>

<script>
import AlertComponent from './components/AlertComponent.vue'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    'alert-component':AlertComponent
  },
  data:function(){
    return{
      alert : {notation:"Working!!"}
    }
  },
  created(){
    axios.get('https://data.food.gov.uk/food-alerts/id/FSA-AA-02-2018.json')
    .then( response => {
        this.alert = response.data
        console.log(response);
    })
    .catch(e => {
       this.errors.push(e)
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
