<template>
  <div>
    <strong style="text:bold">Timer Participants:</strong>
    <a class="button" v-on:click="addParticipant">{{ addMsg }}</a>
    <ul v-for="(participant, participantId) in participantList" :key="participantId" :row-data="participant">
      <li>
      <row v-on:delete-row-event="deleteRow" v-bind:participant="participant"></row>
      <input type="button" v-on:click="deleteRowByIndex(index)" value="Delete"/>
      </li>
    </ul>
  </div>

</template>

<script>
import Row from './Row.vue';
export default {
  components: { Row },
  name: "ParticipantList",
  props: ["bus"],
  data() {
    return {
      eventBus: this.bus,
      participantList: [{id: 1, title: "hello"}, {id: 2, title: "cat mat"}, {id: 3, title:"cat dog"}],
      addMsg: "Add participant",
      deleteMsg: "Delete participant",
      startMsg: "Start",
      name: "Input Name",
      count: 4,
    };
  },

  methods: {
    addParticipant() {
      this.participantList.push({title: this.createName()});
    },
    createName() {
      return this.name + " #" + (this.count++);
    },
    deleteRow(participant) {
      var index = this.participantList.indexOf(participant);
      this.deleteRowByIndex(index);
    },
    deleteRowByIndex(index) {
      this.$children[index].stopTimer();
      console.log("Delete row before", this.participantList, index);
      this.participantList.splice(index, 1);
      //Array.prototype.splice.apply(this.participantList, index, 1);
      console.log("Delete row after", this.participantList);
    }
  },
};
</script>

<style>
button {
  background-color: #4fc08d;
}
a.button {
  padding: 0.55em 2em;
  border-radius: 2em;
  display: inline-block;
  color: #fff;
  background-color: #4fc08d;
  transition: all 0.15s ease;
  box-sizing: border-box;
  border: 1px solid #4fc08d;
  margin: 5px;
}
a:hover {
    cursor: pointer;
}
</style>
