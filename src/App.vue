<template>
  <div id="app">
    <div class="site-container">
      <main class="site-content" id="site-content">
        <CurrencyConverter />
      </main>
      <Footer />
    </div>
  </div>
</template>

<script>
import CurrencyConverter from "./components/CurrencyConverter.vue";
import Footer from "./components/AppFooter.vue";

export default {
  name: "app",
  components: {
    CurrencyConverter,
    Footer
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
  font-size: 18px;
  line-height: 1.333;

  @include media-query($xs-screen) {
    font-size: 20px;
  }

  @include media-query($xl-screen) {
    font-size: 1.333vw;
  }
}

body {
  color: $black;
  background-color: $white;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica,
    Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

small {
  color: $gray;
}

a:hover {
  color: darken($gray, 20);
}

.site-container {
  display: flex;
  flex-direction: column;
  max-width: ms(12);
  min-height: 100vh;
  margin: 0 auto;
  padding: 0 $global-gutter;
}

.site-content {
  flex: 1;
  padding-top: ms(3);
}
</style>
