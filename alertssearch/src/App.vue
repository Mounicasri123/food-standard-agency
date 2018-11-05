<template>
  <div id="app">
    <H1>FSA Food Alerts</H1>
    <div> 
      <div class="search">
        <input type="text" v-model="searchString">
        <input type="submit" value="search" @click="searchApi">
      </div>
      <ol>
      <li v-for="item in alerts.items" :key="item.id">
        <alert-component :item="item"></alert-component>   
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
       axios.get(`https://data.food.gov.uk/food-alerts/id?search=${this.searchString}&_limit=10`)
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

<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.search{
  padding: 5px;
}

</style>
