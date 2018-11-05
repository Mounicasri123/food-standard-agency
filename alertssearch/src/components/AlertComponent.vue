<template>
    <div class="container">
        <!-- <div v-for="item in alert.items" :key="item.id"> -->
        <!-- <ul class="list-group list">
            <li class="list-group-item"> Notation :{{ item.notation }}</li>
            <li class="list-group-item" v-for="problem in item.problem" :key="problem.id">
            Allergen : <span v-for="allergy in problem.allergen" :key="allergy.id">
                            {{allergy.label}}<br>
                        </span>
            </li>
            <li class="list-group-item" v-for="problem in item.problem" :key="problem.id">                      
                            RiskStatement: {{problem.riskStatement}}<br>
            </li>
            <li class="list-group-item" v-for="productDetail in item.productDetails" :key="productDetail.id">
                        Product Name :  {{productDetail.productName}}
            </li>
            <li class="list-group-item">Reporting Business : {{ item.reportingBusiness != null ? item.reportingBusiness.commonName : "" }}</li>
            <li class="list-group-item">Short Title : {{item.shortTitle}}  </li>
            <li class="list-group-item">Alert Type : {{ allergyType }}  </li>
        </ul> -->
        <table>
            <thead></thead>
            <tbody>
                <tr>
                    <td>Notation</td>
                    <td>{{ item.notation }}</td>
                </tr>
                <tr>
                    <td>Allergen :</td> 
                     <td><span v-for="problem in item.problem" :key="problem.id">
                         <span v-for="allergy in problem.allergen" :key="allergy.id">
                            {{allergy.label}}<br>
                        </span>
                        </span>
                    </td>
                </tr> 
                <tr>
                    <td>RiskStatement:</td>                        
                    <td><span v-for="problem in item.problem" :key="problem.id">{{problem.riskStatement}}</span> <br></td>
                    
                </tr>
                <tr>
                    <td>Product Name :  </td> 
                    <td><span v-for="productDetail in item.productDetails" :key="productDetail.id">  {{productDetail.productName}}</span></td>  
                </tr>
                <tr>
                     <td> Reporting Business :</td> 
                     <td>{{ item.reportingBusiness != null ? item.reportingBusiness.commonName : "" }}</td>
                </tr> 
            </tbody>
        </table>
    </div>
    <!-- </div> -->
</template>

<script>
//import axios from 'axios';

export default {
  name: "AlertComponent",
  props: ["item"],
//   data:function(){
//       return{
//           item:{}
//       }
//   },
  computed: {
    allergyType: function() {
      var value = this.item.notation.split("-")[1];
      var result;
      switch (value) {
        case "AA":
          result = "Allergy Alert";
          break;
        case "PRIN":
          result = "Product Recall Information Notice";
          break;
        case "FAFA":
          result = "Food Alert For Action";
          break;
      }
      return result;
    }
  }
//  created(){
//      console.log(this.notation);
//     axios.get(`https://data.food.gov.uk/food-alerts/id/${this.notation}.json`)
//     .then( response => {
//         this.alert = response.data
//         console.log(response);
//     })
//     .catch(e => {
//        this.errors.push(e)
//     })
//   }
};
</script>

<style scoped>
table {
    width: 60%;
    margin-inline-start: 20%;
    max-width: 100%;
    margin-bottom: 20px;
    border: 2px solid #8f8fff;
}
td{
    border: 1px solid #8f8fff;
    padding: 5px;
    }
</style>


