<template>
  <div>
    <button type="button" class="btn btn-primary" @click="getEventData">
      Get event
    </button>
    <div>{{ event }}</div>
  </div>
</template>
<script>
// NEW - import EventService
import EventService from "@/services/EventService.js";
export default {
  name: "EventSingle",
  data() {
    // NEW - initialize the event object
    return {
      event: {},
    };
  },
  created() {
    this.getEventData(); // NEW - call getEventData() when the instance is created
  },
  // NEW
  methods: {
    async getEventData() {
      // Use the eventService to call the getEventSingle() method
      EventService.getEventSingle(this.$route.params.id).then(
        ((event) => {
          this.$set(this, "event", event);
        }).bind(this)
      );
    },
  },
};
</script>
<style lang="scss"></style>
