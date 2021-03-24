<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <hr>
    <button v-on:click="indexProducts">click me</button>
    <div v-if="toggleProducts">
      {{ products }}
    </div>
  </div>
</template>
<style></style>
<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      products: [],
      toggleProducts: false,
    };
  },
  created: function () {},
  methods: {
    indexProducts: function () {
      axios.get("http://localhost:3000/api/products").then((response) => {
        console.log(response.data);
      });
    },
  },
};
</script>