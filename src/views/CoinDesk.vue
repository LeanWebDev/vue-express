<template>
  <div>
    <h1>Bitcoin Price Index</h1>
    <section v-if="errored">
      <p>
        We're sorry, we're not able to retrieve this information at the moment,
        please try back later
      </p>
    </section>

    <section v-else>
      <div v-if="loading">Loading...</div>

      <div
        v-else
        v-for="(currency, index) in info"
        :key="index"
        class="currency"
      >
        {{ currency.description }}:
        <span class="lighten">
          <span v-html="currency.symbol"></span
          >{{ currency.rate_float | currencydecimal }}
        </span>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      info: null,
      loading: true,
      errored: false,
    };
  },
  mounted() {
    this.axios
      .get("https://api.coindesk.com/v1/bpi/currentprice.json")
      .then((response) => (this.info = response.data.bpi))
      .catch((error) => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  },
  filters: {
    currencydecimal(value) {
      return value.toFixed(2);
    },
  },
};
</script>

<style></style>
