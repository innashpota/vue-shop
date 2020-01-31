<template>
  <ul>
    <li v-for="size in sizes" :key="size">{{ size }}</li>
  </ul>
</template>

<script>
export default {
  name: "ProductSizes",
  props: {
    sizes: {
      type: Array,
      required: true
    }
  }
};
</script>