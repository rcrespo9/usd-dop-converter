<template>
  <article>
    <h1>USD to DOP Currency Exchange</h1>
    <input-group>
      <Input
        name="USD"
        :placeholder="USD.base"
        :value="USD.converted"
        country="United States of America"
        flag="us.svg"
        v-on:input="updateExchange"
      />
      <Input
        name="DOP"
        :placeholder="formattedUSDDOP"
        :value="USDDOP.converted"
        country="Dominican Republic"
        flag="do.svg"
        v-on:input="updateExchange"
      />
    </input-group>
    <Info
      :date="lastUpdated"
      convertFrom="1 USD"
      :convertTo="`${formattedUSDDOP} DOP`"
    />
  </article>
</template>

<script>
import axios from "axios";
import { format, parse } from 'date-fns';
import InputGroup from "./CurrencyConverterInputGroup";
import Input from "./CurrencyConverterInput";
import Info from "./CurrencyConverterInfo";

export default {
  name: "CurrencyConverter",
  components: {
    InputGroup,
    Input,
    Info
  },
  data() {
    return {
      USD: {
        base: 1,
        converted: ""
      },
      USDDOP: {
        base: 0,
        converted: ""
      },
      lastUpdated: "",
      loading: true,
      error: false
    };
  },
  created() {
    this.getRecentExchange();
  },
  computed: {
    formattedUSDDOP() {
      return this.formatCurrency(this.USDDOP.base);
    }
  },
  methods: {
    getRecentExchange() {
      const apiKey = process.env.VUE_APP_CURRENCY_API_KEY;
      const endpoint = `http://www.apilayer.net/api/live?access_key=${apiKey}&currencies=DOP`;

      axios
        .get(endpoint)
        .then(response => {
          const {
            success,
            timestamp,
            quotes: { USDDOP }
          } = response.data;
          if (!success) this.error = true;
          this.USDDOP.base = USDDOP;
          this.lastUpdated = format(new Date(timestamp * 1000), 'MM/DD/YYYY');
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
      } else if (name === "DOP") {
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
h1 {
  margin: 0;
  font-size: ms(3);
  font-weight: map-get($font-weight, medium);

  &:after {
    content: "";
    display: block;
    margin: ms(1) 0 ms(-3);
    width: ms(4);
    height: ms(-5);
    background-color: $pink;
  }
}
</style>
