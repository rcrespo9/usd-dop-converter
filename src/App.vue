<template>
  <div id="app">
    <CurrencyConverter />
  </div>
</template>

<script>
import CurrencyConverter from "./components/CurrencyConverter.vue";

export default {
  name: "app",
  components: {
    CurrencyConverter
  }
};
</script>

<style lang="scss">
*,
*:before,
*:after {
  box-sizing: border-box;
}

body {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;  
}
</style>
