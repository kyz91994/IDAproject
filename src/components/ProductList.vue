<template>
  <div class="container">
    <product-item
        v-for="product in products"
        :product="product"
        :key="product.id"
        @removeItem="removeItem"
    />
  </div>
</template>

<script>
import ProductItem from "@/components/ProductItem";
export default {
  name: "ProductList",
  components: {ProductItem},
  props: {
    products: {
      type: Array,
      required: true
    }
  },
  methods:{
    removeItem(productId){
      this.$emit('removeProduct', productId)
}
  }
}
</script>

<style scoped>
.container{
  width: 1028px;
  padding-top: 52px;
  margin-left: 16px;
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
}
</style>