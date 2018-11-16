<template>
  <div id="app">

    <TableInit></TableInit>
    <TableList />
  </div>
</template>

<script>
import TableList from './components/tableList/index.vue'
import TableInit from './components/tableInit/index.vue'

export default {
  name: 'app',
  components: {
    TableList,
    TableInit
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
