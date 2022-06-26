<template>
  <div>
    <div class="adding-form__title">
      Добавление товара
    </div>
    <form @submit.prevent class="adding-form">
      <div class="adding-form__input">
          <span class="adding-form__label">Наименование товара
                <img src="../assets/error_cirlce.png" alt="" class="error-circle">
          </span>
          <custom-input :class="{'error': !product.title.trim()}"
                      placeholder="Введите наименование товара"
                      v-model="product.title"
                        type="text"
          ></custom-input>
          <custom-error-span v-if="!product.title.trim()"></custom-error-span>
      </div>
      <div>
        <span class="adding-form__label">Описание товара</span>
        <custom-text-area placeholder="Введите описание товара"
                          v-model="product.description"
        ></custom-text-area>
      </div>
      <div class="adding-form__input">
        <span class="adding-form__label">Ссылка на изображение товара
         <img src="../assets/error_cirlce.png" alt="" class="error-circle">
        </span>
        <custom-input
            :class="{error: !product.src.trim()}"
            placeholder="Введите ссылку"
            v-model="product.src"
            type="text"
        ></custom-input>
        <custom-error-span v-if="!product.src.trim()"/>
      </div>
      <div class="adding-form__input">
        <span class="adding-form__label">Цена товара
          <img src="../assets/error_cirlce.png" alt="" class="error-circle">
        </span>
        <custom-input
            placeholder="Введите цену"
            v-model="product.price"
            :class="{error: !product.price.trim()}"
            type="text"

        ></custom-input>
        <custom-error-span v-if="!product.price.trim()"></custom-error-span>
      </div>
      <custom-button :class="{'disable': !product.price.trim()|!product.title.trim()|!product.src.trim()}"
                     :disabled="!(product.price.trim()&&product.title.trim()&&product.src.trim())"
                     @click="addProduct"
      >Добавить товар
      </custom-button>
    </form>
  </div>

</template>

<script>
import {v4} from 'uuid'
export default {
  name: "AddProductForm",
  data() {
    return {
      product: {
        title: '',
        description: '',
        src: '',
        price: '',
      },
    }
  },
  methods: {
    addProduct() {
      this.product.id = v4()
      this.$emit('addProduct', this.product)
      this.product = {
        title: '',
        description: '',
        src: '',
        price: '',
      }
    },
    setError(){
      if(!this.product.title||!this.product.src||!this.product.price){
        this.error = true
      }
    }
  }
}
</script>

<style scoped lang="scss">
.adding-form {
  width: 332px;
  height: 440px;
  padding: 24px;
  background: #FFFEFB;
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;

  &__title {
    width: 247px;
    height: 35px;
    font-weight: 600;
    font-size: 28px;
    line-height: 35px;
    color: #3F3F3F;
    margin-bottom: 17px;
  }

  &__input {
    display: flex;
    flex-direction: column;
    height: 66px;
    gap: 5px;
  }

  &__label {
    font-style: normal;
    font-weight: 400;
    font-size: 10px;
    line-height: 13px;
    letter-spacing: -0.02em;
    color: #49485E;
  }
}

.error-circle {
  width: 4px;
  height: 4px;
  border-radius: 4px;
  background-color: #FF8484;
}
</style>