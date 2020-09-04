<template>
  <div id="app" class="text-center">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/events">Events</router-link> |
      <router-link to="/event/1">Single event</router-link>
    </div>
    <div v-if="loading">Loading...</div>
    <div v-if="!loading && !error">Welcome</div>
    <div v-if="!loading && error">Some error has occurred</div>
    <router-view />
  </div>
</template>
<script>
import { mapActions } from "vuex";

export default {
  data() {
    return {
      loading: true,
      error: false,
    };
  },
  methods: {
    ...mapActions(["initialLoad"]),
  },
  async mounted() {
    try {
      await this.initialLoad();
    } catch (err) {
      this.loading = false;
      this.error = true;
      console.log(err);
    }
  },
};
</script>
<style></style>
