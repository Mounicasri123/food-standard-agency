<template>
  <div id="app">
    <div> 
      <input type="text" v-model="searchString" @input="searchApi">
      <ol>
      <li v-for="item in alerts.items" :key="item.id">
        <alert-component :notation="item.notation"></alert-component>   
      </li>
    </ol>
    </div>    
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
      alerts : {},
      searchString:''
    }
  },
  methods:{
    searchApi(event){
       axios.get(`https://data.food.gov.uk/food-alerts/id?search=${event.target.value}&_limit=10`)
    .then( response => {
        this.alerts = response.data;
        console.log(response);
    })
    .catch(e => {
       this.errors.push(e)
    })
    }
  },  
  created(){
    axios.get('https://data.food.gov.uk/food-alerts/id?_limit=10')
    .then( response => {
        this.alerts = response.data;
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
