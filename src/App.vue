<template>
  <div id="app">
    <div class="nav-bar"></div>
    <Product product="Socks" 
             image="https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg"
             link="https://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=socks"/>
  </div>
</template>

<script>
import Product from "./components/Product.vue";
export default {
  name: "app",
  components: {
    Product
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
  background: linear-gradient(-90deg, #84CF6A, #16C0B0);
  height: 60px;
  margin-bottom: 15px;
}
</style>