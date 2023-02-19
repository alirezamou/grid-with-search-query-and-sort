<script>
</script>

<template>
  <div class="container">
    <div class="search-query">
      <label for="">Search</label>
      <input type="text">
    </div>
    <table class="table">
      <thead>
        <th>Name</th>
        <th>Power</th>
      </thead>
      <tbody>
        <tr>
          <td>Chuck Norris</td>
          <td>Infinity</td>
        </tr>
        <tr>
          <td>bruce lee</td>
          <td>9000</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>

.container {
  padding: 0.5rem;
}

.search-query {
  margin-bottom: 0.5rem;
}

table {
  border: solid #42b983 2px;
  border-radius: 2px;
}

th {
  background-color: #42b983;
  color: #fff;
  font-weight: bold;
}

td {
  background-color: #f9f9f9;
}

th, td {
  padding: 0.5rem 2rem;
}



</style>
