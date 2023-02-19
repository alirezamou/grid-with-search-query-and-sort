<script>
export default {
    props: {
        data: Array,
        columns: Array
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
        <th v-for="c in columns">{{ upperCaseFirstLetter(c) }}</th>
      </thead>
      <tbody>
        <tr v-for="d in data" :key="d.id">
          <td v-for="column in columns">{{ typeof d[column] === "string" ? upperCaseFirstLetter(d[column]) : d[column] }}</td>
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