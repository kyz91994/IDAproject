<template>
<textarea class="custom-textarea"
          :value="modelValue"
          @input="updateTextArea"></textarea>
</template>

<script>
export default {
  name: "CustomTextArea",
  props: {
    modelValue: [String]
  },
  methods: {
    updateTextArea(event) {
      this.$emit('update:modelValue', event.target.value)
    }
  }
}
</script>

<style scoped lang="scss">
.custom-textarea{
  padding: 14px 18px;
  width: 284px;
  height: 108px;
  border-radius: 4px;
  background-color: #FFFEFB;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  font-size: 12px;
  font-weight: 400;
  font-style: normal;
  line-height: 15px;
  color: #3F3F3F;
  resize: none;
&::-webkit-input-placeholder{
   font-weight: 400;
   font-size: 12px;
   line-height: 15px;
   color: #B4B4B4;
 }
&::-moz-placeholder{
   font-weight: 400;
   font-size: 12px;
   line-height: 15px;
   color: #B4B4B4;
 }
&:-ms-input-placeholder{
   font-weight: 400;
   font-size: 12px;
   line-height: 15px;
   color: #B4B4B4;
 }

}
</style>