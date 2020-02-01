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

    <div v-show="selectedTab === 'Reviews'">
      <p v-if="!reviews.length">There are no reviews yet.</p>
      <ul v-else>
        <li v-for="(review, index) in reviews" :key="index">
          <p>{{ review.name }}</p>
          <p>Rating: {{ review.rating }}</p>
          <p>Review: {{ review.review }}</p>
          <p>Recommend: {{ review.recommend }}</p>
        </li>
      </ul>
    </div>

    <div v-show="selectedTab === 'Make a Review'">
      <ProductReview />
    </div>
  </div>
</template>

<script>
import ProductReview from "./ProductReview.vue";

export default {
  name: "ProductTabs",
  components: {
    ProductReview
  },
  props: {
    reviews: {
      type: Array,
      required: false
    }
  },
  data() {
    return {
      tabs: ["Reviews", "Make a Review"],
      selectedTab: "Reviews"
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
