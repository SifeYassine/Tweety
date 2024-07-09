<template>
  <SideBar />
</template>

<style>
body {
  background-color: black;
}
</style>

<script>
// import { ref, onMounted } from "vue";
// import axios from "axios";
import "../src/style.css";
import SideBar from "./components/SideBar.vue";

export default {
  name: "App",
  components: {
    SideBar,
  },
};
</script>
