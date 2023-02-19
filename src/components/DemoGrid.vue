<script>
export default {
  data() {
    return {
      sortOrders: this.columns.reduce((acc, currentVal) => {
        acc[currentVal] = 1;
        return acc;
      }, {}),
      sortKey: ""
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
      },
      sortBy (key) {
        this.sortKey = key;
        this.sortOrders[key] *= -1;
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
          tData = tData.slice().sort((a, b) => {
            a = a[this.sortKey];
            b = b[this.sortKey];
            return (a === b ? 0 : a > b ? 1 : -1) * this.sortOrders[this.sortKey];
          });
          return tData;
      }
  }
}
</script>

<template>
     <table v-if="filteredData.length !== 0">
      <thead>
        <tr>
          <th v-for="c in columns" @click="sortBy(c)" :class="{active : sortKey == c}">{{ upperCaseFirstLetter(c) }}
              <span class="arrow" :class="sortOrders[c] > 0 ? 'asc' : 'dsc'"></span>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="d in filteredData" :key="d.id">
          <td v-for="column in columns">{{ typeof d[column] === "string" ? upperCaseFirstLetter(d[column]) : d[column] }}</td>
        </tr>
      </tbody>
    </table>
    <div v-else>No matches found</div>
</template>

<style scoped>
table {
  border: solid #42b983 2px;
  border-radius: 2px;
}

th {
  background-color: #42b983;
  color: rgba(255, 255, 255, 0.66);
  font-weight: bold;
  cursor: pointer;
}

th.active {
  color: #fff;
}

th.active .arrow {
  opacity: 1;
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