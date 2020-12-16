<template>
  <mdb-container class="text-center animated fadeIn">
    <h1 class="title">
      Currency Checker
    </h1>
    <hr />

    <mdb-row  class="justify-content-md-center">
      <mdb-col  sm="12" md="6" >
        <ComponentA />
      </mdb-col>
      <mdb-col  sm="12"  md="6">
        <ComponentB />
      </mdb-col>
    </mdb-row>
  </mdb-container>
</template>

<script>
import { mdbContainer, mdbRow, mdbCol } from "mdbvue";

import Logo from "~/components/Logo.vue";
import ComponentA from "~/components/ComponentA.vue";
import ComponentB from "~/components/ComponentB.vue";

export default {
  components: {
    Logo,
    mdbContainer,
    mdbRow,
    mdbCol,
    ComponentA,
    ComponentB,
  },
};
</script>

<style>
.container {
  margin: 10vh auto 0 auto;
  min-height: 90vh;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 80px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
}

.links {
  padding-top: 15px;
}
</style>
