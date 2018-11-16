<template>
    <transition name="modal">
        <div class="modal-mask">
            <div class="modal-wrapper">
                <div class="modal-container">
                    <div class="modal-header">
                        <slot name="header">
                             FSA Food Alerts INFO          
                        </slot>
                    </div>
            
                    <div class="modal-body">
                        <slot name="body">
                            <table>
                                <tbody>
                                    <tr>
                                            <td>Notation:</td>
                                            <td><span v-for="item in alert.items" :key="item.id">{{item.notation}}</span></td>
                                    </tr>
                                    <hr>
                                    <tr>
                                        <td>SMS Text :</td>
                                        <td><span v-for="item in alert.items" :key="item.id">{{item.SMStext}}</span></td>
                                    </tr>
                                    <hr>
                                    <tr>
                                        <td>Description:</td>
                                        <td><span v-for="item in alert.items" :key="item.id">{{item.description}}</span></td>
                                    </tr>
                                </tbody>
                            </table>
                        </slot>
                     </div>
                    <div class="modal-footer">
                         <slot name="footer">
                             <button class="modal-default-button" @click="$emit('close')">
                                 close
                             </button>
                        </slot>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
import axios from 'axios';

  export default {
    name: 'SingleAlert',
    props:['notation'],
    data:function(){
        return{
            alert:{}
        }
    },
    // methods: {
    //   close() {
    //     this.$emit('close');
    //   },
    // },
    created(){
     console.log(this.notation);
    axios.get(`https://data.food.gov.uk/food-alerts/id/${this.notation}.json`)
    .then( response => {
        this.alert = response.data
        console.log(response.data);
    })
    .catch(e => {
       this.errors.push(e)
    })
     }
  };
</script>
<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, .5);
  display: table;
  transition: opacity .3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 70%;
  margin: 0px auto;
  /* padding: 20px 30px; */
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
  transition: all .3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  color: #4AAE9B;;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
    color: white;
    background: #4AAE9B;
    border: 1px solid #4AAE9B;
    border-radius: 2px;
}

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

</style>