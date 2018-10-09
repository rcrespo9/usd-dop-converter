<template>
  <label>{{name}}
    <input type="number" :name="name" :placeholder="placeholder" :value="value" @input="updateExchange" min="0">
  </label>  
</template>

<script>
export default {
  name: 'CurrencyConvertInput',
  props: {
    name: {
      type: String,
      required: true
    },
    placeholder: {
      type: Number,
      required: true
    },
    value: {
      type: String,
      required: true
    }
  },
  methods: {
    updateExchange() {
      this.$emit('input', event);
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
