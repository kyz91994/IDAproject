<template>
  <div class="container">
    <custom-select3
        :options="sortOptions"
        :default="'По умолчанию'"
        @changeOption="sortedProducts"
        class="custom-select__item"
        v-if="products.length"
    />
    <transition-group name="product-list">
      <product-item
          v-for="product in products"
          :product="product"
          :key="product.id"
          @removeItem="removeItem"
          class="product-item"
      />
    </transition-group>

  </div>
</template>

<script>
import ProductItem from "@/components/ProductItem";
import CustomSelect3 from "@/components/UI/CustomSelect3";
export default {
  name: "ProductList",
  components: {CustomSelect3, ProductItem},
  data(){
    return{
      sortOptions: [
        {value: 'default', name: 'По умолчанию'},
        {value: 'title', name: 'По названию'},
        {value: 'price', name: 'По цене min'},
        {value: 'priceMax', name: 'По цене max'}
      ],
      selectedSort: ''
    }
  },
  props: {
    products: {
      type: Array,
      required: true
    }
  },
  methods:{
    removeItem(productId){
      this.$emit('removeProduct', productId)
    },
    sortedProducts(option){
      this.selectedSort = option.value
      this.$emit('sortedProducts', option.value)
    }
  }
}
</script>

<style scoped>
.container{
  max-width: 1028px;
  padding-top: 52px;
  margin-left: 16px;
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
  position: relative;
}
.custom-select__item{
  position: absolute;
  top: 0;
  right: 0
}
.product-list-item {
  display: flex;
  margin-right: 10px;
}
.product-list-enter-active,
.product-list-leave-active {
  transition: all 0.6s ease;
}
.product-list-enter-from,
.product-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}
.post-list-move {
  transition: transform 0.8s ease;
}
</style>