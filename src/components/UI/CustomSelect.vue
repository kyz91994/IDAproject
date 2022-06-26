<template>
  <select class="custom-select" @change="changeOption">
    <option value="" disabled selected>Выберите из списка</option>
    <option
        v-for="option in options"
        :key="option.value"
        :value="option.value"
    >{{option.name}}</option>
  </select>
</template>

<script>
export default {
  name: "custom-select",
  props: {
    modelValue:{
      type: String
    },
    options: {
      type: Array,
      default: ()=>[]
    }
  },
  methods: {
    changeOption(event){
      this.$emit('update:modelValue', event.target.value)
  },
  }
}
</script>

<style scoped>
.custom-select{
  height: 40px;
  outline: none;
  /*align-self: flex-end;*/
}
</style>