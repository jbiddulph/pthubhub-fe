<template>
  <div>
    <label for="selector">
      Filter:
      <select v-model="selectedFilter" id="selector">
        <option value="all" selected>All</option>
        <option value="Purchased">Purchased</option>
        <option value="Unpurchased">Unpurchased</option>
        <option value="One time purchases">One time purchases</option>
        <option value="subscriptions">Subscriptions</option>
      </select>
    </label>
    <h1>SELECTED FILTER: {{ selectedFilter }}</h1>
    <div class="products-list">
      <div v-for="(product, idx) in products" :key="idx">
        <Product :product="product" />
      </div>
    </div>
  </div>
</template>

<script>
const productItems = require("@/assets/products.json");
import Product from "../components/Product.vue";

export default {
  name: "ProductList",
  components: {
    Product
  },
  data() {
    return {
      selectedFilter: "all",
      currentOrder: "order"
    };
  },
  computed: {
    products() {
      let productList = [...productItems];
      switch (this.selectedFilter) {
        case "Purchased":
          productList = productList.filter(item => {
            return item.purchased == true;
          });
          return productList;
        case "Unpurchased":
          productList = productList.filter(item => {
            return item.purchased == false;
          });
          return productList;
        case "One time purchases":
          productList = productList.filter(item => {
            return item.type == "onetime";
          });
          return productList;
        case "subscriptions":
          productList = productList.filter(item => {
            return item.type == "recurring";
          });
          return productList;
        default:
          return productList;
      }
    }
  },
  watch: {
    selectedFilter: function(newVal) {
      this.selectedFilter = newVal;
    }
  }
};
</script>

<style scoped>
.products-list {
  display: flex;
  justify-content: center;
  flex-direction: row;
  max-width: 1600px;
  margin: 0 auto;
  flex-wrap: wrap;
}
</style>
