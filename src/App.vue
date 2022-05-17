<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <Table :userData="userData"></Table>
  </div>
</template>

<script>
import Table from "../src/components/table.vue";
export default {
  name: "App",
  components: { Table },
  data() {
    return {
      userData: [
        {
          name: "王小虎",
          sex: "男",
          phone: "111111111111",
          id: 1,
        },
        {
          name: "王小虎",
          sex: "男",
          phone: "111111111111",
          id: 2,
        },
        {
          name: "王小虎",
          sex: "男",
          phone: "111111111111",
          id: 3,
        },
        {
          name: "王小虎",
          sex: "男",
          phone: "111111111111",
          id: 4,
        },
      ],
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
