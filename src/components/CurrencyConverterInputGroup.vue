<template>
  <div class="currency-input-group">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "CurrencyInputGroup"
};
</script>

<style lang="scss" scoped>
.currency-input:first-of-type {
  border-bottom: 2px solid rgba($white, 0.5);
}
</style>
