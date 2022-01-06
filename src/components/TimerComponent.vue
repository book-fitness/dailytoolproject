<template>
<div style="display:inline-block">
  <input type="text" v-model="seconds" />
  <input type="text" v-model="participant.title" />
</div>
</template>

<script>
export default {
  props: ["participant"],
  data() {
    return {
      minutes: 20000,
      seconds: 100,
      interval: null,
      //partic: this.participant,
    };
  },
  // mounted() {
  //   var _this = this;
  //   console.log("mounted");
  //   this.eventBus.$on("participant-start-timer-event", function(event) {_this.count(); console.log(event)});
  // },
  unmounted() {
    console.log("Timer unmounted");
  },
  deactivated() {
    console.log("Timer deactivated");
  },
  destroyed() {
    console.log("Timer destroyed");
  },
  methods: {
    count() {
      console.log("count");
      if (this.seconds != 0) {
        this.seconds--;
      } else if (this.minutes != 0) {
        this.minutes--;
        this.seconds = 59;
      } else {
        this.stop();
      }
    },
    tick() {
      this.count();
    },
    start() {
      console.log("start");
      var _this = this;
      this.interval = setInterval(function () {
        _this.tick();
      }, 1000);
    },
    stop() {
      console.log("stop", this.interval);
      if (this.interval == null) return;
      clearInterval(this.interval);
      this.interval = null;
      
    },
  },
};
</script>

<style>
</style>