<template>
  <footer>
    <small>{{convertFrom}} = {{convertTo}}</small>
  </footer>
</template>

<script>
export default {
  name: "CurrencyConverterInfo",
  props: {
    convertFrom: {
      type: String,
      required: true
    },
    convertTo: {
      type: String,
      required: true
    }
  }
};
</script>

<style lang="scss" scoped>
footer {
  text-align: right;
}

small {
  font-size: ms(-1);
}
</style>
