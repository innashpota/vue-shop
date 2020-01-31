<template>
  <div id="app">
    <div class="nav-bar"></div>
    <Product :premium="premium" />
  </div>
</template>

<script>
import Product from "./components/Product.vue";
export default {
  name: "app",
  components: {
    Product
  },
  data() {
    return {
      premium: true
    };
  }
};
</script>

<style>
body {
  font-family: tahoma;
  color: #282828;
  margin: 0px;
}

.nav-bar {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
  height: 60px;
  margin-bottom: 15px;
}
</style>