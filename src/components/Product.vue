<template>
  <div>
    <h1>{{ product }}</h1>
  </div>
</template>

<script>
export default {
  name: "Product",
  props: {
    product: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  margin: 4vh 0 0;
}
</style>