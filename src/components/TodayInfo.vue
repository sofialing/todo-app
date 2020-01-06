<template>
  <header class="text-center mb-4">
    <h1 class="display-3 font-weight-normal">{{ time }}</h1>
    <span class="lead font-weight-light">Today is {{ date }}</span>
  </header>
</template>

<script>
import moment from "moment";

export default {
  name: "TodayInfo",
  data() {
    return {
      date: moment().format("dddd, MMMM Do YYYY"),
      time: moment().format("HH:mm")
    };
  },
  created() {
    setInterval(this.updateClock, 1000);
  },
  methods: {
    updateClock() {
      this.time = moment().format("HH:mm");
    }
  }
};
</script>
