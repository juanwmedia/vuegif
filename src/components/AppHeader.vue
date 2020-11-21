<template>
  <header class="header">
    <form class="search" @submit.prevent="searchGifs">
      <input
        v-model="searchTerm"
        type="search"
        class="search__input"
        placeholder="Search for gifs 🙀..."
        required
      />
      <input type="button" @click="$emit('clear-search')" value="Clear" />
      <input type="submit" value="Search" class="search__submit" />
    </form>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  data() {
    return {
      searchTerm: "",
    };
  },
  methods: {
    searchGifs() {
      this.$emit("search-gifs", this.searchTerm);
    },
  },
};
</script>

<style scoped>
/* Header */
.header {
  margin-bottom: 3rem;
}
.search {
  display: flex;
}
.search__input {
  width: 100%;
  padding: 0.6rem;
  font-size: 1.3rem;
}
</style>
