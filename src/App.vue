<template>
  <div id="app" class="text-center">
    <ul id="nav" class="nav nav-tabs justify-content-center">
      <li class="nav-item">
        <router-link to="/" class="nav-link"></router-link>
      </li>
      <li class="nav-item">
        <router-link to="/events" class="nav-link">Events</router-link>
      </li>
      <li class="nav-item">
        <router-link to="/event/1" class="nav-link">Single event</router-link>
      </li>
      <li class="nav-item">
        <router-link to="/coindesk" class="nav-link">CoinDesk</router-link>
      </li>
    </ul>
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
