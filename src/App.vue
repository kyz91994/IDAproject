<template>
<div class="app">
  <add-product-form
      @addProduct="addProduct"
  />
  <product-list
      @removeProduct="removeProduct"
      :products="sortedProducts"
      @sortedProducts="setSelectedSort"
      v-if="!postsLoading"
  />
  <div v-else>
    <img src="./assets/preloader.svg"/>
  </div>
</div>
</template>
<script>
import AddProductForm from "@/components/AddProductForm";
import ProductList from "@/components/ProductList";
export default {
  components: {ProductList, AddProductForm},
  data(){
    return{
      products: [],
      selectedSort: 'default',
      postsLoading: false
    }
  },
  methods: {
    addProduct(product){
      this.products.push(product)
      sessionStorage.setItem(product.id, JSON.stringify(product))
    },
    removeProduct(productId){
      this.products = this.products.filter(prod=> prod.id !== productId)
      sessionStorage.removeItem(productId)
    },
    setSelectedSort(value){
      this.selectedSort = value
    }
  },
  mounted(){
    this.postsLoading = true
    if(sessionStorage.length){
      this.products = [...Object.values(sessionStorage)].map(prod=> JSON.parse(prod)).sort()
    }
    this.postsLoading = false
  },
  computed:{
    sortedProducts(){
      const products = this.products.map(product=> ({...product}))
      if(this.selectedSort==='priceMax'){
        return [...products].sort((post1, post2) =>post1['price']-post2['price']).reverse()
      }else if(this.selectedSort === 'default') {
        return [...products]
      }else if(this.selectedSort==='price'){
        return [...products].sort((post1, post2) =>post1[this.selectedSort]-post2[this.selectedSort])
      }else {
       return [...products.sort((post1, post2) =>post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))]
      }
    }
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
</style>