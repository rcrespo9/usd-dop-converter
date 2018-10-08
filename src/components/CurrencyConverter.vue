<template>
  <div>
    <label>USD
      <input type="number" name="USD" :placeholder="USD.base" v-model.number="USD.converted" min="1">
    </label>

    <label>USDDOP
      <input type="number" name="USDDOP" :placeholder="USDDOP.base" v-model.number="USDDOP.converted" min="1">
    </label>
  </div>
</template>

<script>
import axios from "axios";
import _ from "lodash";

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
  watch: {
    USD: {
      handler(newVal) {
        const { converted } = newVal;
        const convertedVal = this.convertUSDDOP(converted);

        this.USDDOP.converted = parseFloat(convertedVal) || "";
      },
      deep: true
    },
    USDDOP: {
      handler(newVal) {
        const { converted } = newVal;
        const convertedVal = this.convertUSD(converted);

        this.USD.converted = parseFloat(convertedVal) || "";
      },
      deep: true
    }
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
    convertUSD(newVal) {
      const { base } = this.USDDOP;
      const convertedVal = newVal / base;
      const formattedVal = this.formatCurrency(convertedVal);

      return formattedVal;
    },
    convertUSDDOP(newVal) {
      const { base } = this.USDDOP;
      const convertedVal = newVal * base;
      const formattedVal = this.formatCurrency(convertedVal);

      return formattedVal;
    },
    formatCurrency(val) {
      return parseFloat(val).toFixed(2);
    }
  }
};
</script>

<style lang="scss" scoped>
</style>
