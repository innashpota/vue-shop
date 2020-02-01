<template>
  <div>
    <ul>
      <span
        class="tabs"
        :class="{ activeTab: selectedTab === tab }"
        v-for="(tab, index) in tabs"
        @click="selectedTab = tab"
        :key="index"
      >{{ tab }}</span>
    </ul>

    <div v-show="selectedTab === 'Shipping'">
      <p>Shipping : {{ shipping }}</p>
    </div>

    <div v-show="selectedTab === 'Details'">
      <ProductDetails :details="details" />
    </div>

    <div v-show="selectedTab === 'Sizes'">
      <ProductSizes :sizes="sizes" />
    </div>
  </div>
</template>

<script>
import ProductDetails from "./ProductDetails.vue";
import ProductSizes from "./ProductSizes.vue";

export default {
  name: "InfoTabs",
  components: {
    ProductDetails,
    ProductSizes
  },
  props: {
    shipping: {
      required: true
    },
    details: {
      type: Array,
      required: true
    },
    sizes: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      tabs: ["Shipping", "Details", "Sizes"],
      selectedTab: "Shipping"
    };
  }
};
</script>

<style scoped>
.tabs {
  margin-left: 20px;
  cursor: pointer;
}

.activeTab {
  color: #16c0b0;
  text-decoration: underline;
}
</style>
