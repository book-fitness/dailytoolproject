<template>
<div style="display:inline-block">
  <input type="text" v-model="text" />
</div>
</template>

<script>
export default {
  props: ["participant"],
  data() {
    return {
      text: "text",
    };
  },

  methods: {

  },
};
</script>

<style>
</style>