<template>
  
</template>

<script>
import axios from 'axios';

export default {
  name: 'CurrencyConverter',
  data () {
    return {
      exchange: '',
      loading: true,
      error: false
    }
  },
  created () {
    this.getRecentExchange();
  },
  methods: {
    getRecentExchange () {
      const apiKey = process.env.VUE_APP_CURRENCY_API_KEY;
      const endpoint = `http://www.apilayer.net/api/live?access_key=${apiKey}&currencies=DOP`;

      axios.get(endpoint)
        .then(response => this.exchange = response.data)
        .catch(error => {
          console.log(error);
          this.error = true;
        })
        .finally(() => this.loading = false);
    }
  }
}
</script>

<style lang="scss" scoped>

</style>

