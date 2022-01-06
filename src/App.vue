<template>
  
  <div>
    <input  v-if="commonRoom == false" type="button" value="go to chat" v-on:click="goToCommonRoom"/>
  <div v-if="commonRoom == true">
    <common-chat></common-chat>
  </div>
  </div>
    <!-- <participant-list v-bind:bus="bus"></participant-list> -->
  
  <!-- <timer></timer> -->
</template>

<script>
// import ParticipantList from "./components/ParticipantList.vue";
import CommonChat from "./components/CommonChat.vue";
import Vue from "vue";
// import Timer from "./components/Timer.vue";
export default {
  data() {
    return {
      bus: new Vue(),
      commonRoom: false
    }
  }, 
  methods: {
    goToCommonRoom() {
      console.log("go to room")
      this.commonRoom = true;
    },
  },
  name: 'App',
  components: {
    CommonChat
    // ParticipantList,
    //Timer,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
textarea {
  width: 70%;
  height: 300px;
}
</style>
