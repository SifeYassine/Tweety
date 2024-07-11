<template>
  <SideBar />
  <div class="flex">
    <main class="w-[51vw] ml-[20vw] border-2 border-blue-500">
      <h2
        class="h-10 text-xl font-bold text-white border-[1px] border-[lightgray]"
      >
        Home
      </h2>
      <TweetBar />
      <PostsContainer />
    </main>
    <div>
      <SearchField />
      <TrendingBar />
    </div>
  </div>
</template>

<style>
body {
  background-color: black;
}

main {
  margin-right: 25px;
}
</style>

<script>
// import { ref, onMounted } from "vue";
// import axios from "axios";
import "../src/style.css";
import SideBar from "./components/SideBar.vue";
import TrendingBar from "./components/Trending.vue";
import SearchField from "./components/SearchField.vue";
import TweetBar from "./components/TweetBar.vue";
import PostsContainer from "./components/Posts.vue";

export default {
  name: "App",
  components: {
    SideBar,
    TrendingBar,
    SearchField,
    TweetBar,
    PostsContainer,
  },
};
</script>
