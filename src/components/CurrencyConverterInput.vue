<template>
  <label>{{name}}
    <input type="number" :name="name" :placeholder="placeholder" :value="value" @input="inputEvt">
  </label>  
</template>

<script>
export default {
  name: 'CurrencyConvertInput',
  props: {
    name: String,
    placeholder: Number,
    value: Number,
    inputEvt: Function
  }
}
</script>

<style lang="scss" scoped>

</style>
