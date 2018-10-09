<template>
  <div>
    <Input
      name="USD"
      :placeholder="USD.base"
      :value="USD.converted"
      v-on:input="updateExchange"
    />
    <Input
      name="USDDOP"
      :placeholder="USDDOP.base"
      :value=USDDOP.converted
      v-on:input="updateExchange"
    />
  </div>
</template>

<script>
import axios from "axios";
import Input from "./CurrencyConverterInput";

export default {
  name: "CurrencyConverter",
  components: {
    Input
  },
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
      const { name, value } = e.target;
      let convertedVal;
      let formattedVal;

      if (name === "USD") {
        convertedVal = value * base;
        formattedVal = this.formatCurrency(convertedVal);

        this.USD.converted = value;
        this.USDDOP.converted = formattedVal > 1 ? formattedVal : "";
      } else if (name === "USDDOP") {
        convertedVal = value / base;
        formattedVal = this.formatCurrency(convertedVal);

        this.USDDOP.converted = value;
        this.USD.converted = formattedVal > 1 ? formattedVal : "";
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
