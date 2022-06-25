<template>
<div class="app">
  <add-product-form></add-product-form>
  <div class="container">
    <product-card></product-card>
    <product-card></product-card>
    <product-card></product-card>
    <product-card></product-card>
    <product-card></product-card>
    <product-card></product-card>
    <product-card></product-card>
    <product-card></product-card>
    <product-card></product-card>
  </div>

</div>
</template>
<script>


import ProductCard from "@/components/ProductCard";
import AddProductForm from "@/components/AddProductForm";
export default {
  components: {AddProductForm, ProductCard}
}
</script>
<style lang="scss">
#app {
  font-family: 'Source Sans Pro';
  padding: 31px;
}
.app{
  display: flex;
  justify-content: flex-start;
}
.container{
  width: 1028px;
  padding-top: 52px;
  margin-left: 16px;
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
}
</style>