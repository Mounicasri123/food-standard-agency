<template>
    <div class="container">
        <div v-for="item in alert.items" :key="item.id">

        
    <ol class="list-group list">
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
        <li class="list-group-item">Reporting Business : {{item.reportingBusiness.commonName}}</li>
        <li class="list-group-item">Short Title : {{item.shortTitle}}  </li>
        <li class="list-group-item">Alert Type : {{ allergyType }}  </li>
    </ol>
    </div>
    </div>
</template>

<script>
export default {
  name: "AlertComponent",
  props: ["alert"],
  computed: {
    allergyType: function() {
      var value = this.alert.items[0].notation.split("-")[1];
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
};
</script>

<style>
ol.list{
    border: 2px solid #8f8fff;
}
</style>


