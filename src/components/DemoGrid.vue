<script>
export default {
    props: {
        data: Array
    },
    methods: {
        upperCaseFirstLetter (str) {
            return str.split(" ").map(item => `${item.charAt(0).toUpperCase()}${item.slice(1)}`).join(" ");
        }
    }
}
</script>

<template>
     <table class="table">
      <thead>
        <th>Name</th>
        <th>Power</th>
      </thead>
      <tbody>
        <tr v-for="person in data" :key="person.id">
          <td>{{ upperCaseFirstLetter(person.name) }}</td>
          <td>{{ person.power }}</td>
        </tr>
      </tbody>
    </table>
</template>

<style scoped>
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