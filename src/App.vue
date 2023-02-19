<script>
import DemoGrid from './components/DemoGrid.vue';
export default {
  components: {
    DemoGrid
  },
  data() {
    return {
      gridColumns: ['name', 'power'],
      gridData: [
        {id: 1, name: 'chuck norris', power: Infinity},
        {id: 1, name: 'bruce lee', power: 9000},
        {id: 1, name: 'jackie chan', power: 7000},
        {id: 1, name: 'jet li', power: 6000},
      ]
    }
  }
}
</script>

<template>
  <div class="container">
    <div class="search-query">
      <label for="">Search</label>
      <input type="text">
    </div>
    <DemoGrid :data="gridData" :columns="gridColumns"/>
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
