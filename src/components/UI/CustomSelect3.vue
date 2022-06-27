<template>
  <div class="custom-select"
       @click="isOptionsVisible=!isOptionsVisible">
    <div class="custom-select__title"
    >{{ selected }}
      <img src="../../assets/arrow.svg" class="custom-select__arrow" alt="arr">
    </div>
    <div class="custom-select__options"
         v-if="isOptionsVisible">
      <div class="custom-select__option"
           v-for="option in options"
           :key="option.value"
           @click="changeOption(option)"
           @click.stop
      >{{ option.name }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CustomSelect3",
  data() {
    return {
      isOptionsVisible: false,
      selected: this.default
    }
  },
  props: {
    modelValue: {
      type: String
    },
    default: {
      type: String,
      required: true
    },
    options: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    changeOption(option) {
      this.$emit('update:modelValue', option.value)
      this.$emit('changeOption', option)
      this.selected = option.name
      this.isOptionsVisible = false
    },
  }
}
</script>

<style scoped lang="scss">
.custom-select {
  width: 200px;
  height: 36px;
  outline: none;
  padding: 11px 5px 11px 11px;
  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  color: #B4B4B4;
  background: #FFFEFB;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  position: relative;

  &:hover {
    cursor: pointer;
  }

  &__title {
    display: flex;
    align-items: center;
  }

  &__arrow {
    position: absolute;
    right: 13px;
  }

  &__options {
    position: absolute;
    top: 38px;
    right: 0;
    width: 100%;
    outline: none;
    color: #B4B4B4;
    background: #FFFEFB;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    z-index: 1;
  }

  &__option {
    text-align: center;
    padding: 11px 0;
    cursor: pointer;
  }

  &__option:hover {
    background-color: dodgerblue;
    border-radius: 4px;
    cursor: pointer;
  }
}
</style>