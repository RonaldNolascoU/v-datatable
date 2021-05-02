<template>
  <DataTable />
</template>

<script>
import DataTable from './components/DataTable'
export default {
  name: "App",
  components: {DataTable}
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
