<template>
  <div class="container">
    <h1 class="text-center">Məhsul Əlavə et</h1>
    <hr />
    <New-Product></New-Product>
        <br /><br />
    <progress-bar></progress-bar>
    <br /><br />
    <progress-bar v-if="show"></progress-bar>
    <br /><br />
    
    <hr />
  <product-list></product-list>
  </div>
</template>

<script>
import NewProduct from "./components/NewProduct.vue";
import ProgressBar from "./components/ProgressBar.vue";
import ProductList from './components/ProductsList.vue'
export default {
  components: {
    "New-Product": NewProduct,
    ProgressBar,
    ProductList,
   
  },
  data() {
    return {
      imageList: [],
      product: {
        selectedImage: null,
      },
    };
  },
};
</script>

<style>
body {
  background-color: aliceblue;
  padding-top: 20px;
  padding-bottom: 20px;
}

.card {
  margin-right: 5px;
  margin-bottom: 5px;
}

.card:last-child {
  margin-right: 0px;
}

.col-md-2 {
  max-width: 15.666667% !important;
}

.product-container {
  margin-left: 15px;
}
</style>
