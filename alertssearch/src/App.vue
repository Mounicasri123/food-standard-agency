<template>
  <div id="app">     
    <alert-component :alert="alert"></alert-component>   
  </div>
</template>

<script>
import AlertComponent from './components/AlertComponent.vue'

export default {
  name: 'app',
  components: {
    'alert-component':AlertComponent
  },
  data:function(){
    return{
      alert : {notation:"Working!!"}
    }
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
