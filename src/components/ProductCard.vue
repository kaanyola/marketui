<template>
  <div class="product-container">
    <img :src="product.photo" />
    <div class="details">
      <button v-on:click="addOrRemoveFavorite(product)">
        {{ getButtonName }}
      </button>
      <p class="product-name">{{ product.product }}</p>
      <p class="product-name">{{ getPrice }}</p>
      <p>{{ product.description }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "ProductCard",
  props: ["product", "favoriteProducts"],
  computed: {
    getPrice() {
      return `${this.product.price} $`;
    },
    getButtonName() {
      return this.favoriteProducts.find(
        (item) => item.favorited === this.product.id
      )
        ? `Remove Favorite`
        : `Add Favorite`;
    },
  },
  mounted(){
      console.log(this.favoriteProducts)
  },
  methods: {
    addOrRemoveFavorite(product) {
      if (this.favoriteProducts.find((item) => item.favorited === product.id)) {
          let index = this.favoriteProducts.findIndex((item) => item.favorited === product.id)
          let item = this.favoriteProducts.find((item) => item.favorited === product.id)

            this.favoriteProducts.splice(index, 1);
        axios
          .delete("http://127.0.0.1:8000/favorited/" + item.id + "/")
          .then((response) => {
            console.log(response); 
            console.log(this.favoriteProducts);
          });
      } else {
        product["favorited"] = product.id;
        console.log(this.favoriteProducts)
        axios
          .post("http://127.0.0.1:8000/favorited/", product)
          .then(function (response) {
            console.log(response);
            this.favoriteProducts = [this.favoriteProducts]
            
          })
          .catch(function (error) {
            console.log(error);
          });
      }
    },
  },
};
</script>

<style>
.product-container {
  width: 40%;
  display: flex;
  margin: 30px;
  border: 2px solid black;
}
img {
  width: 300px;
  height: 300px;
}

.product-name {
  font-weight: bold;
  font-size: 20px;
}
</style>