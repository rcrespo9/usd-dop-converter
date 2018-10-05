<template>
  <div>
    <input type="number" name="USD" id="USD">
    <input type="number" name="USDDOP" id="USDDOP">
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "CurrencyConverter",
  data() {
    return {
      exchange: "",
      USDDOP: "",
      loading: true,
      error: false
    };
  },
  created() {
    this.getRecentExchange();
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
    }
  }
};
</script>

<style lang="scss" scoped>
</style>