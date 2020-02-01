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

      <InfoTabs :shipping="shipping" :details="details" :sizes="sizes" />

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

    <ProductTabs :reviews="reviews" />
  </div>
</template>

<script>
import ProductTabs from "./ProductTabs.vue";
import InfoTabs from "./InfoTabs.vue";
import { eventBus } from "../main.js";

export default {
  name: "Product",
  components: {
    ProductTabs,
    InfoTabs
  },
  props: {
    premium: {
      type: Boolean,
      required: true
    },
    product: {
      type: String,
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
      sizes: ["S", "M", "L", "XL", "XXL", "XXXL"],
      reviews: []
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
  },
  mounted() {
    eventBus.$on("review-submitted", productReview => {
      this.reviews.push(productReview);
    });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.product {
  display: flex;
  flex-flow: wrap;
  padding: 1rem;
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0px 0.5px 1px #d8d8d8;
}

.product-image {
  width: 80%;
}

.product-image,
.product-info {
  margin-top: 10px;
  width: 50%;
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

.reviews {
  width: 47%;
}
</style>
