<template>
  <div id="app">

    <!-- <TableInit></TableInit> -->
    <TableList />
    <!-- <AddIns></AddIns> -->
    <!-- <tree></tree> -->
  </div>
</template>

<script>
import TableList from "./components/tableList/index.vue";
import TableInit from "./components/tableInit/index.vue";
// import Rizhi from "./components/rizhi/index.vue";
// import RizhiSingle from "./components/rizhi/single.vue";
// import XunJian from "./components/xunJian/index.vue";
// import AddIns from "./components/xunJian/addIns.vue";
import Tree from "./components/tree/index.vue";

export default {
  name: "app",
  components: {
    TableList,
    TableInit,
    // Rizhi,
    // RizhiSingle,
    // XunJian,
    // AddIns,
    Tree
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
