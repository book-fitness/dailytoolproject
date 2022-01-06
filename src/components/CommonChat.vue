<template>
  <div>
    <textarea v-model="message"></textarea>
    <input type="button" value="sendmessage" v-on:click="sendMessage" />
    <ul v-for="(m, index) in messages" :key="index">
      <li>{{ m }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      ws: null,
      message: "",
      messages: [],
    };
  },
  mounted() {
    // this.createSocket();
  },
  created() {
    // var _this = this;
    //this.onMessage();
    this.createSocket();
    //this.onMessage();
    //this.sendMessage();
  },
  methods: {
    sendMessage() {
      console.log(this.isOpen(this.ws));
      this.ws.send(this.message);

    },
    onMessage() {
      console.log("onMessage()", this.ws.onmessage);
    },
    createSocket() {
      this.ws = new WebSocket("ws://localhost:8080/websocket");
      console.log(this.ws);
      var _this = this;
      this.ws.onmessage = function (event) {
        console.log("event data", event.data);
        console.log("message", _this.message);
        _this.messages.push(event.data);
      };
    },
    isOpen(ws) {
      return ws.readyState === ws.OPEN;
    },
  },
};
</script>
