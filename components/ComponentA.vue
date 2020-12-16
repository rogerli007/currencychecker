<template>
  <div>
    <h2>
      This is Component A
    </h2>

    <div class="form-group">
      <label for="Start-Date">Start Date (yyyy-mm-dd)</label>
      <input
        type="text"
        id="Start-Date"
        class="form-control"
        v-model="dateStart"
      />
    </div>
    <div class="form-group">
      <label for="End-Date">End Date (yyyy-mm-dd)</label>
      <input type="text" id="End-Date" class="form-control" v-model="dateEnd" />
    </div>
    <div class="form-group">
      <label for="Currency-A"
        >Currency base
        <span>
          <mdb-tooltip trigger="hover" :options="{ placement: 'top' }">
            <span slot="tip"> {{ currencyItems_sorted }} </span>
            <a slot="reference"> (Currency Supported)</a>
          </mdb-tooltip></span
        ></label
      >
      <input
        type="text"
        id="Currency-A"
        class="form-control"
        v-model="currencyBase"
      />
    </div>
    <div class="form-group">
      <label for="Currency-B"
        >Currency to check
        <span>
          <mdb-tooltip trigger="hover" :options="{ placement: 'top' }">
            <span slot="tip"> {{ currencyItems_sorted }} </span>
            <a slot="reference"> (Currency Supported)</a>
          </mdb-tooltip></span
        ></label
      >
      <input
        type="text"
        id="Currency-B"
        class="form-control"
        v-model="currencyCheck"
      />
    </div>
    <mdb-btn color="default" @click="submit">Submit</mdb-btn>
    <p class="red-text">
      {{ err_msg }}
    </p>
  </div>
</template>

<script>
import { mapMutations } from "vuex";
import { mdbBtn, mdbAutocomplete, mdbDatePicker2, mdbTooltip } from "mdbvue";
export default {
  computed: {
    todos() {
      return this.$store.state.todos.list;
    },
    currencyItems_sorted() {
      var obj = this.currencyItems;
      return obj.sort();
    },
  },
  components: {
    mdbBtn,
    mdbAutocomplete,
    mdbDatePicker2,
    mdbTooltip,
  },
  data() {
    return {
      dateStart: "",
      dateEnd: "",
      currencyBase: "",
      currencyCheck: "",
      state: "",
      err_msg: "",
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

      rates: {},
    };
  },

  methods: {
    submit() {
      var that = this;
      // `this` will refer to the component instance

      fetch(
        "https://api.exchangeratesapi.io/history?start_at=" +
          this.dateStart +
          "&end_at=" +
          this.dateEnd +
          "&symbols=" +
          this.currencyBase.toUpperCase() +
          "," +
          this.currencyCheck.toUpperCase() +
          "&base=" +
          this.currencyBase.toUpperCase() +
          ""
      )
        .then((response) => {
          if (response.ok) {
            return response.json();
          } else {
            throw new Error("Network response was not ok.");
          }
        })
        .then((data) => {
          that.rates = data.rates;
          that.storeResult(that.rates);

          that.err_msg = "";
        })
        .catch(function(error) {
          that.err_msg = error.message;
          that.storeResult({});
          console.log(
            "There has been a problem with your fetch operation: ",
            error.message
          );
        });
    },
    storeResult(obj) {
      this.$store.commit("todos/update", obj);
    },
    ...mapMutations({
      toggle: "todos/toggle",
    }),
  },
};
</script>

<style lang="scss" scoped></style>
