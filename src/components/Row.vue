<template>
    <div>
      <input type="text" v-bind:value="participant.title" />
      <timer :participant="participant"></timer>
      <row-info :participant="participant"></row-info>
      <a class="button" v-on:click="startTimer()">{{startMsg}}</a> 
      <a class="button" v-on:click="deleteParticipant()">{{deleteMsg}}</a> 
    </div>
</template>

<script>
import Timer from "./TimerComponent.vue";
import RowInfo from "./RowInfoComponent.vue";
export default {
  components: { Timer, RowInfo },
  name: "Row",
  props: ["participant"],
  data() {
    return { 
      addMsg: "Add participant",
      deleteMsg: "Delete participant",
      startMsg: "Start",
      name: "Input Name",
      //partic: this.participant,
    };
  },
  unmounted() {
    console.log("Row unmounted");
  },
  deactivated() {
    console.log("Row deactivated");
  },
  destroyed() {
    console.log("Row destroyed", this.participant.title);
    this.stopTimer();
  },
  methods: {
    deleteParticipant() {
      console.log("delete", this.participant.title);
      this.$emit("delete-row-event", this.participant)
    },
    startTimer() {
      console.log("start timer", this.$children);
      //this.eventBus.$emit("participant-start-timer-event", this.index);
      //this.$children[index].start();
      for (var i = 0; i < this.$children.length; i++) {
          if ('start' in this.$children[i]) {
              this.$children[i].start();
          }
      }
    },
    stopTimer() {
        console.log("stop timer");
        for (var i = 0; i < this.$children.length; i++) {
          if ('stop' in this.$children[i]) {
              this.$children[i].stop();
          }
      }
    }
  }
}
</script>


