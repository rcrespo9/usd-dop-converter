<template>
  <footer>
    <small>Last Updated: {{date}}</small>
    <small>{{convertFrom}} = {{convertTo}}</small>
  </footer>
</template>

<script>
export default {
  name: "CurrencyConverterInfo",
  props: {
    date: {
      type: String,
      required: true
    },
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
  display: flex;
  justify-content: space-between;
}

small {
  font-size: ms(-1);
}
</style>
