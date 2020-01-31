<template>
  <ul>
    <li v-for="detail in details" :key="detail">{{ detail }}</li>
  </ul>
</template>

<script>
export default {
  name: "ProductDetails",
  props: {
    details: {
      type: Array,
      required: true
    }
  }
};
</script>
