<template>
  <div>
    <h2>
      This is Component B
    </h2>

    <div>
      <div v-for="(i, k) in orderedResult" :key="k">
        <h3>{{ k }}</h3>
        <p>{{ Object.keys(i)[0] }}: {{ i[Object.keys(i)[0]].toFixed(2) }}</p>
        <p>{{ Object.keys(i)[1] }}: {{ i[Object.keys(i)[1]].toFixed(2) }}</p>
      </div>
    </div>
    <p v-if="!orderedResult">
      {{ orderedResult }}
    </p>
  </div>
</template>

<script>
import { mdbBtn, mdbAutocomplete, mdbDatePicker2 } from "mdbvue";
export default {
  components: {
    mdbBtn,
  },
  computed: {
    orderedResult() {
      var obj = this.$store.state.todos.list;
      if (typeof obj !== "undefined" && obj != null) {
        return Object.keys(obj)
          .sort()
          .reduce(function(result, key) {
            result[key] = obj[key];
            return result;
          }, {});
      }
    },
  },
  data() {
    return {
      rates: {},
      dateStart: "",
      dateEnd: "",
      currencyBase: "",
      currencyCheck: "",
      currencyItems: [
        "CAD",
        "HKD",
        "ISK",
        "PHP",
        "DKK",
        "HUF",
        "CZK",
        "GBP",
        "RON",
        "SEK",
        "IDR",
        "INR",
        "BRL",
        "RUB",
        "HRK",
        "JPY",
        "THB",
        "CHF",
        "EUR",
        "MYR",
        "BGN",
        "TRY",
        "CNY",
        "NOK",
        "NZD",
        "ZAR",
        "USD",
        "MXN",
        "SGD",
        "AUD",
        "ILS",
        "KRW",
        "PLN",
      ],
    };
  },

  methods: {
    submit() {
      fetch(
        "https://api.exchangeratesapi.io/history?start_at=2018-01-01&end_at=2018-09-01&symbols=ILS,JPY&base=HKD"
      )
        .then((response) => response.json())
        .then((data) => (this.rates = data.rates));
    },
  },
};
</script>

<style lang="scss" scoped></style>
