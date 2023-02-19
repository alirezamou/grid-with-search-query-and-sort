<script>
import DemoGrid from './components/DemoGrid.vue';
export default {
  components: {
    DemoGrid
  }
}
</script>

<template>
  <div class="container">
    <div class="search-query">
      <label for="">Search</label>
      <input type="text">
    </div>
    <DemoGrid />
  </div>
</template>

<style scoped>

.container {
  padding: 0.5rem;
}

.search-query {
  margin-bottom: 0.5rem;
}

</style>
