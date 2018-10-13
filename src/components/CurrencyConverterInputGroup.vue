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
// .currency-input-group {
//   margin-bottom: ms(-3);
// }

.currency-input:first-of-type {
  border-bottom: 2px solid rgba($gray, 0.5);
}
</style>
