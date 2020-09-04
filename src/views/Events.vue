<template>
  <div class="about">
    <h1>Events list</h1>
    <div class="list-group">
      <router-link
        v-for="event in events"
        :key="event.id"
        tag="a"
        :to="'event/' + event.id"
        class="list-group-item list-group-item-action"
        >{{ event.name }}</router-link
      >
    </div>
  </div>
</template>
<script>
// NEW - import EventService
import EventService from "@/services/EventService.js";
export default {
  name: "Events",
  data() {
    // NEW - initialize the event object
    return {
      events: [],
    };
  },
  created() {
    this.getEvents(); // NEW - call getEventData() when the instance is created
  },
  // NEW
  methods: {
    async getEvents() {
      // Use the eventService to call the getEventSingle() method
      EventService.getEvents().then(
        ((events) => {
          this.$set(this, "events", events);
        }).bind(this)
      );
    },
  },
};
</script>
