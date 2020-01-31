<template>
  <div id="app">
    <div class="nav-bar"></div>
    <div class="cart">
      <p>Cart({{ cart.length }})</p>
    </div>
    <Product
      :premium="premium"
      :cart="cart"
      @add-to-cart="addToCart"
      @remove-from-cart="removeFromCart"
    />
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
      premium: true,
      cart: []
    };
  },
  methods: {
    addToCart(id) {
      this.cart.push(id);
    },
    removeFromCart(id) {
      const index = this.cart.indexOf(id);
      this.cart.splice(index, 1);
    }
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

.cart {
  margin-right: 25px;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 5px 20px;
}
</style>