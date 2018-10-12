<template>
  <footer>
    <small>&copy; {{getYear}} <a href="https://rudycrespo.com">Rudy Crespo</a></small>
  </footer>
</template>

<script>
export default {
  name: 'AppFooter',
  computed: {
    getYear() {
      const date = new Date();
      return date.getFullYear();
    }
  }
}
</script>

<style lang="scss" scoped>
footer {
  padding: ms(1) 0;
}

small {
  font-size: ms(-1);
}

a {
  color: inherit;
  font-weight: map-get($font-weight, semi-bold);
  text-decoration: none;
}
</style>


