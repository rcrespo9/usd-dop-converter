<template>

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
