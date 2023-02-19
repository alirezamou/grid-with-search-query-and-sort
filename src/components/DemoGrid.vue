<script>
export default {
  data() {
    return {
      sortOrders: { name: 1 }
    }
  },
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
          // first sort array on `name` column in ascending order
          tData = tData.slice().sort((a, b) => {
            a = a.name;
            b = b.name;
            return (a === b ? 0 : a > b ? 1 : -1) * this.sortOrders.name;
          });
          return tData;
      }
  }
}
</script>

<template>
     <table class="table">
      <thead>
        <tr>
          <th @click="sortOrders.name *= -1" v-for="c in columns">{{ upperCaseFirstLetter(c) }}
              <span class="arrow" :class="sortOrders.name === 1 ? 'asc' : 'dsc'"></span>
          </th>
        </tr>
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

.arrow {
  display: inline-block;
  vertical-align: middle;
  width: 0;
  height: 0;
  margin-left: 5px;
  opacity: 0.66;
}

.arrow.asc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-bottom: 4px solid #fff;
}

.arrow.dsc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-top: 4px solid #fff;
}

</style>