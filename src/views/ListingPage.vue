<template>
  <div class="main-container">
      <ProductCard v-for="product in products" :key="product.id" :product="product" :favoriteProducts="favoriteProducts"/>
  </div>
</template>

<script>
import axios from "axios";
import ProductCard from "../components/ProductCard.vue";

export default {
  name: "ListingPage",
  components: {
      ProductCard
  },
  data() {
    return {
      products: null,
      favoriteProducts: []
    };
  },
  mounted(){
      axios.get("http://127.0.0.1:8000/product/").then((response) => this.products = response.data.results);
      axios.get("http://127.0.0.1:8000/favorited/").then((response) => this.favoriteProducts = response.data.results);
  }
};
</script>

<style>
.main-container{
    width: 70%;
    height: auto;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  flex-wrap: wrap;
}
</style>