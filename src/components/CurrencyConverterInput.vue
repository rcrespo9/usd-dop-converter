<template>
  <div class="currency-input">
    <label>
      <span class="currency-input__label">
        <img :src="require(`@/assets/${flag}`)" :alt="`${country} flag`" class="label__img">
        <span class="label__name">{{name}}</span>
      </span>
      <input type="number" :name="name" :placeholder="placeholder" :value="value" @input="updateExchange" min="1">
    </label>
  </div> 
</template>

<script>
export default {
  name: "CurrencyConverterInput",
  props: {
    name: {
      type: String,
      required: true
    },
    placeholder: {
      type: Number,
      required: true
    },
    value: {
      type: String,
      required: true
    },
    country: {
      type: String,
      required: true
    },
    flag: {
      type: String,
      required: true
    }
  },
  methods: {
    updateExchange() {
      this.$emit("input", event);
    }
  }
};
</script>

<style lang="scss" scoped>
.currency-input {
  padding: ms(2) 0;
}

.currency-input__label,
input {
  display: block;
}

.currency-input__label {
  display: grid;
  grid-template-columns: ms(0) 1fr;
  grid-gap: ms(-3);
  align-items: center;
  margin-bottom: ms(-1);
  font-size: ms(0);
  font-weight: map-get($font-weight, medium);
  letter-spacing: ms(-13);
  text-transform: uppercase;
}

.label__img {
  width: 100%;
  height: auto;
  border-radius: 2px;
}

input {
  padding: 0;
  border: none;
  background-color: transparent;
  font-size: ms(4);
}
</style>
