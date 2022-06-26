<template>
<div class="app">
  <add-product-form
      @addProduct="addProduct"
  />
  <product-list
      @removeProduct="removeProduct"
      :products="products"
  />
</div>
</template>
<script>
import AddProductForm from "@/components/AddProductForm";
import ProductList from "@/components/ProductList";
export default {
  components: {ProductList, AddProductForm},
  data(){
    return{
      products: []
    }
  },
  methods: {
    addProduct(product){
      this.products.push(product)
      sessionStorage.setItem(product.id, JSON.stringify(product))
      console.log(sessionStorage)
    },
    removeProduct(productId){
      this.products = this.products.filter(prod=> prod.id !== productId)
      sessionStorage.removeItem(productId)
    }
  },
  mounted(){
    this.products = [...Object.values(sessionStorage).sort()].map(prod=> JSON.parse(prod))
  }
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
//.container{
//  width: 1028px;
//  padding-top: 52px;
//  margin-left: 16px;
//  display: flex;
//  gap: 16px;
//  flex-wrap: wrap;
//}
</style>