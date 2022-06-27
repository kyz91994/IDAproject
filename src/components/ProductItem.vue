<template>
  <div class="product" @mouseover="mouseOn = true" @mouseleave="mouseOn = false">
    <div class="product__image-body">
      <button v-show="mouseOn" @click="removeItem(product.id)" class="product__remove">
        <img class="product__delete" src="../assets/delete-button.svg" alt="remove_btn">
      </button>
      <img class="product__photo" src="../assets/product.jpg" alt="">
    </div>
    <div class="product__body">
      <div class="product__title">
        {{ product.title }}
      </div>
      <div class="product__description">
        <div class="product__text">
          {{ product.description }}
        </div>
      </div>
      <div class="product__price">
        {{ product.price.replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1 ') }} руб.
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductItem",
  data() {
    return {
      mouseOn: false
    }
  },
  props: {
    product: {
      type: Object,
      required: true
    }
  },
  methods: {
    removeItem(productId) {
      this.$emit('removeItem', productId)
    },
  }
}
</script>

<style scoped lang="scss">
.product {
  width: 332px;
  height: 423px;
  background: #FFFEFB;
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  display: flex;
  flex-direction: column;

  &:hover {
    cursor: url('../assets/hover.svg'), default;
  }

  &__image-body {
    position: relative;
    object-fit: cover;
  }

  &__photo {
    border-radius: 4px 4px 0px 0px;;
  }

  &__body {
    height: 222px;
    display: flex;
    flex-direction: column;
    padding: 21px 16px 29px 16px;
  }

  &__title {
    font-style: normal;
    font-weight: 600;
    font-size: 20px;
    line-height: 25px;
    color: #3F3F3F;
    align-self: flex-start;
  }

  &__description {
    display: flex;
    flex: 1 1 auto;
    padding-top: 24px;
    font-style: normal;
    font-weight: 400;
    font-size: 16px;
    line-height: 20px;
    color: #3F3F3F;
    flex-direction: row;
  }

  &__text {
    width: 100%;
    height: 100%;
    overflow: auto;
    word-wrap: break-word;
  }

  &__price {
    font-style: normal;
    padding-top: 5px;
    font-weight: 600;
    font-size: 24px;
    line-height: 30px;
    color: #3F3F3F;
    align-self: start;
  }

  &__remove {
    border: none;
    position: absolute;
    top: -8px;
    right: -8px;
    background: none;
    &:hover {
      cursor: url('../assets/hover.svg'), default;
    }
  }

}
</style>