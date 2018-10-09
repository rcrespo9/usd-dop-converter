<template>
  <div id="app">
    <div class="site-container">
      <main class="site-content" id="site-content">
        <CurrencyConverter />
      </main>
    </div>
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

html {
  font-size: 20px;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica,
    Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.site-container {
  max-width: ms(12);
  margin: 0 auto;
  padding: 0 $global-gutter;
}
</style>
