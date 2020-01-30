<template>
  <div class="product">
    <div class="product-image">
      <img :src="image" />
    </div>

    <div class="product-info">
      <h1>{{ product }}</h1>
      <p v-if="inStock">In Stock</p>
      <p v-else>Out of Stock</p>
      <span v-if="onSale">On Sale!</span>

      <ul>
        <li v-for="detail in details" :key="detail">{{ detail }}</li>
      </ul>

      <ul>
        <li v-for="size in sizes" :key="size">{{ size }}</li>
      </ul>

      <div v-for="variant in variants" :key="variant.variantId">
        <p @mouseover="updateProduct(variant.variantImage)">{{ variant.variantColor }}</p>
      </div>

      <button v-on:click="addToCart">Add to cart</button>
      <button @click="removeFromCart">Remove from cart</button>

      <div class="cart">
        <p>Cart({{ cart }})</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Product",
  props: {
    product: String
  },
  data() {
    return {
      image:
        "https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg",
      inStock: true,
      onSale: false,
      details: ["80% cotton", "20% polyester", "Gender-neutral"],
      variants: [
        {
          variantId: 2234,
          variantColor: "green",
          variantImage:
            "https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg"
        },
        {
          variantId: 2235,
          variantColor: "blue",
          variantImage:
            "https://www.vuemastery.com/images/challenges/vmSocks-blue-onWhite.jpg"
        }
      ],
      sizes: ["S", "M", "L", "XL", "XXL", "XXXL"],
      cart: 0
    };
  },
  methods: {
    addToCart() {
      this.cart += 1;
    },
    updateProduct(variantImage) {
      this.image = variantImage;
    },
    removeFromCart() {
      this.cart -= 1;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.product {
  display: flex;
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0px 0.5px 1px #d8d8d8;
}

.product-image {
  flex-basis: 700px;
}

.product-info {
  margin-top: 10px;
  flex-basis: 500px;
}

.color-box {
  width: 40px;
  height: 40px;
  margin-top: 5px;
}

.cart {
  margin-right: 25px;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 5px 20px;
}

button {
  margin-top: 30px;
  border: none;
  background-color: #1e95ea;
  color: white;
  height: 40px;
  width: 100px;
  font-size: 14px;
}

.disabledButton {
  background-color: #d8d8d8;
}

.review-form {
  width: 30%;
  padding: 20px;
  border: 1px solid #d8d8d8;
}

input {
  width: 100%;
  height: 25px;
  margin-bottom: 20px;
}

textarea {
  width: 100%;
  height: 60px;
}
</style>