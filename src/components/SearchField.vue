<template>
  <!-- Search Field -->
  <input
    type="text"
    placeholder="Search Twitter"
    class="w-full h-10 mt-6 mb-4 pl-4 border-[1px] border-[lightgray] rounded-full"
    v-model="searchQuery"
    @keyup.enter="search"
  />
</template>

<script>
export default {
  name: "SearchField",
  data() {
    return {
      searchQuery: "",
    };
  },
  methods: {
    search() {
      this.$emit("search", this.searchQuery);
    },
  },
};
</script>
