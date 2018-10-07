<template>
  <div>
    <label>USD
      <input type="number" name="USD" v-model.number="USD.converted">
    </label>

    <label>USDDOP
      <input type="number" name="USDDOP" v-model.number="USDDOP.converted">
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
        converted: 1
      },
      USDDOP: {
        base: 48.96,
        converted: 48.96
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
        this.updateUSDDOP(newVal.converted);
      },
      deep: true
    },
    USDDOP: {
      handler(newVal) {
        this.updateUSD(newVal.converted);
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
    updateUSD(newVal) {
      const { base } = this.USDDOP;
      const convertedVal = newVal / base;
      this.USD.converted = convertedVal;
    },
    updateUSDDOP(newVal) {
      const { base } = this.USDDOP;
      const convertedVal = newVal * base;
      this.USDDOP.converted = convertedVal;
    }
  }
};
</script>

<style lang="scss" scoped>
</style>
