<template>
  <div>
    <div class="search-results--header">
      <SearchBar />
    </div>
    <div v-if="$nuxt.context.query.q" class="search-results">
      <SearchResults />
    </div>
  </div>
</template>

<script>
export default {}
</script>
<style>
.search-results--header {
  display: flex;
  justify-content: center;
  padding: 3rem;
}
</style>
