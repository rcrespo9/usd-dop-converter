<template>
  <div>
    <label>USD
      <input type="number" name="USD" :placeholder="USD.base" :value="USD.converted" @input="updateExchange">
    </label>

    <label>USDDOP
      <input type="number" name="USDDOP" :placeholder="USDDOP.base" :value="USDDOP.converted" @input="updateExchange">
    </label>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "CurrencyConverter",
  data() {
    return {
      exchange: "",
      USD: {
        base: 1,
        converted: ""
      },
      USDDOP: {
        base: 48.96,
        converted: ""
      },
      loading: true,
      error: false
    };
  },
  created() {
    // this.getRecentExchange();
  },
  methods: {
    getRecentExchange() {
      const apiKey = process.env.VUE_APP_CURRENCY_API_KEY;
      const endpoint = `http://www.apilayer.net/api/live?access_key=${apiKey}&currencies=DOP`;

      axios
        .get(endpoint)
        .then(response => {
          if (!response.data.success) this.error = true;
          this.exchange = response.data;
          this.USDDOP = response.data.quotes.USDDOP;
        })
        .catch(() => (this.error = true))
        .finally(() => (this.loading = false));
    },
    updateExchange(e) {
      const { base } = this.USDDOP;
      const { name, valueAsNumber } = e.target;
      let convertedVal;
      let formattedVal;

      if (name === "USD") {
        convertedVal = valueAsNumber * base;
        formattedVal = this.formatCurrency(convertedVal);

        this.USD.converted = valueAsNumber;
        this.USDDOP.converted = formattedVal;
      } else if (name === "USDDOP") {
        convertedVal = valueAsNumber / base;
        formattedVal = this.formatCurrency(convertedVal);

        this.USDDOP.converted = valueAsNumber;
        this.USD.converted = formattedVal;
      }
    },
    formatCurrency(val) {
      return parseFloat(val).toFixed(2);
    }
  }
};
</script>

<style lang="scss" scoped>
</style>
