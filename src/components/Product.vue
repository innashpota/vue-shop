<template>
  <div class="product">
    <div class="product-image">
      <img :src="image" />
    </div>

    <div class="product-info">
      <h1>{{ title }}</h1>
      <p v-if="inStock">In Stock</p>
      <p v-else :class="{ outOfStock: !inStock }">Out of Stock</p>
      <p>{{ sale }}</p>
      <p>Shipping : {{ shipping }}</p>

      <ProductDetails :details="details" />

      <ProductSizes :sizes="sizes" />

      <div
        v-for="(variant, index) in variants"
        :key="variant.variantId"
        class="color-box"
        :style="{ backgroundColor: variant.variantColor }"
        @mouseover="updateProduct(index)"
      ></div>

      <button
        v-on:click="addToCart"
        :disabled="!inStock"
        :class="{ disabledButton: !inStock }"
      >Add to cart</button>
      <button
        @click="removeFromCart"
        :disabled="cart.length === 0"
        :class="{ disabledButton: cart.length === 0 }"
      >Remove from cart</button>
    </div>
  </div>
</template>

<script>
import ProductDetails from "./ProductDetails.vue";
import ProductSizes from "./ProductSizes.vue";
export default {
  name: "Product",
  components: {
    ProductDetails,
    ProductSizes
  },
  props: {
    premium: {
      type: Boolean,
      required: true
    },
    product: {
      type: String,
      required: true,
      default: "Socks"
    },
    cart: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      onSale: true,
      brand: "Vue Mastery",
      selectedVariant: 0,
      details: ["80% cotton", "20% polyester", "Gender-neutral"],
      variants: [
        {
          variantId: 2234,
          variantColor: "green",
          variantImage:
            "https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg",
          variantQuantity: 10
        },
        {
          variantId: 2235,
          variantColor: "blue",
          variantImage:
            "https://www.vuemastery.com/images/challenges/vmSocks-blue-onWhite.jpg",
          variantQuantity: 0
        }
      ],
      sizes: ["S", "M", "L", "XL", "XXL", "XXXL"]
    };
  },
  methods: {
    addToCart() {
      this.$emit("add-to-cart", this.selectedVariantId);
    },
    updateProduct(index) {
      this.selectedVariant = index;
    },
    removeFromCart() {
      this.$emit("remove-from-cart", this.selectedVariantId);
    }
  },
  computed: {
    title() {
      return this.brand + " " + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].variantImage;
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity;
    },
    sale() {
      if (this.onSale) {
        return this.brand + " " + this.product + " are on sale!";
      }
      return this.brand + " " + this.product + " are not on sale";
    },
    shipping() {
      return this.premium ? "Free" : "2.99";
    },
    selectedVariantId() {
        return this.variants[this.selectedVariant].variantId;
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

button {
  margin-top: 30px;
  margin-right: 5px;
  border: none;
  background-color: #1e95ea;
  color: white;
  height: 40px;
  width: 150px;
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