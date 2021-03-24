<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <hr>
    <button v-on:click="indexProducts">click me</button>
    <div v-bind:key= "product.id" v-for="product in products">
      <p v-if="toggleProducts"> {{product.name}} - {{ product.description }} </p>
    </div>
    <hr>
    <input v-model="productName" placeholder="enter name"/>
    <input v-model="productDescription" placeholder="enter description"/>
    <input v-model="productPrice" placeholder="enter price"/>
    <button v-on:click="createProduct">create product </button>

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
      productName: "",
      productDescription: "",
      productPrice: "",
      productImageUrl: "#",
    };
  },
  created: function () {},
  methods: {
    indexProducts: function () {
      axios.get("http://localhost:3000/api/products").then((response) => {
        console.log(response.data);
        this.products = response.data;
        this.toggleProducts = !this.toggleProducts;
      });
    },
    createProduct: function () {
      var params = {
        name: this.productName,
        description: this.productDescription,
        price: this.productPrice,
        image_url: this.productImageUrl,
      };
      axios.post("http://localhost:3000/api/products", params).then((response) => {
        console.log(response.data);
        this.products.push(response.data);
        this.products.name = "";
        this.products.description = "";
        this.products.price = "";
        this.products.image_url = "";
      });
    },
    testVariables: function () {
      console.log(this.productName);
    },
  },
};
</script>