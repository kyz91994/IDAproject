<template>
<span class="custom-span__error">Поле является обязательным</span>
</template>

<script>
export default {
  name: "CustomErrorSpan"
}
</script>

<style scoped lang="scss">
.custom-span__error{
  //position: absolute;
  //width: 100px;
  //height: 10px;
  //left: 56px;
  //top: 315px;
  font-style: normal;
  font-weight: 400;
  font-size: 8px;
  line-height: 10px;
  letter-spacing: -0.02em;
  color: #FF8484;
}
</style>