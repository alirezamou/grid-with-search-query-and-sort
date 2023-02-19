<script>
export default {
    props: {
        data: Array,
        columns: Array,
        filterKey: String
    },
    methods: {
        upperCaseFirstLetter (str) {
            return str.split(" ").map(item => `${item.charAt(0).toUpperCase()}${item.slice(1)}`).join(" ");
        }
    },
    computed: {
        filteredData () {
            let tData = this.data;
            if(this.filterKey) {
                const fKey = this.filterKey.toLowerCase();
                tData = this.data.filter(row => {
                    return Object.keys(row).some(key => {
                        return String(row[key]).toLowerCase().indexOf(fKey) > -1
                    });
                });
            }
            return tData;
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
        <tr v-for="d in filteredData" :key="d.id">
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