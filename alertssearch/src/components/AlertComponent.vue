<template>
    <div class="container">
         <span v-for="item in alert.items" :key="item.id">{{item.notation}}</span>
    </div>
</template>

<script>
export default {
    name:'AlertComponent',
    props:['alert']
}
</script>

<style>

</style>


