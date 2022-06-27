<template>
  <div>
    <div class="adding-form__title">
      Добавление товара
    </div>
    <form @submit.prevent class="adding-form">
      <div class="adding-form__input">
        <label class="adding-form__label">Наименование товара
          <img src="../assets/error_cirlce.png" alt="" class="error-circle">
        </label>
        <custom-input :class="{'error': isTitleError}"
                      placeholder="Введите наименование товара"
                      v-model="product.title"
                      type="text"
                      @blur="isFieldTouched = true"
        />
        <custom-error-span v-if="isTitleError"/>
      </div>
      <div>
        <label class="adding-form__label">Описание товара</label>
        <custom-text-area placeholder="Введите описание товара"
                          v-model="product.description"
        />
      </div>
      <div class="adding-form__input">
        <label class="adding-form__label">Ссылка на изображение товара
          <img src="../assets/error_cirlce.png" alt="" class="error-circle">
        </label>
        <custom-input
            :class="{error: isSrcError}"
            placeholder="Введите ссылку"
            v-model="product.src"
            type="text"
            @blur="isFieldTouched = true"
        />
        <custom-error-span v-if="isSrcError"/>
      </div>
      <div class="adding-form__input">
        <label class="adding-form__label">Цена товара
          <img src="../assets/error_cirlce.png" alt="" class="error-circle">
        </label>
        <custom-input
            placeholder="Введите цену"
            v-model="product.price"
            :class="{error: isPriceError}"
            @blur="isFieldTouched = true"
            type="number"
        />
        <custom-error-span v-if="isPriceError"/>
      </div>
      <custom-button :class="{'disable': disabledBtn}"
                     :disabled="disabledBtn"
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
      isFieldTouched: false
    }
  },
  methods: {
    addProduct() {
      this.product.id = v4();
      this.$emit('addProduct', this.product);
      this.product = {
        title: '',
        description: '',
        src: '',
        price: '',
      };
      this.isFieldTouched = false
    },
  },
  computed: {
    isPriceError() {
      return this.isFieldTouched && !this.product.price.trim()
    },
    isSrcError() {
      return this.isFieldTouched && !this.product.src.trim()
    },
    isTitleError() {
      return this.isFieldTouched && !this.product.title.trim()
    },
    isFormEmpty() {
      return !this.product.title.trim() | !this.product.src.trim() | !this.product.price.trim()
    },
    disabledBtn() {
      return this.isSrcError | this.isTitleError | this.isPriceError | this.isFormEmpty
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