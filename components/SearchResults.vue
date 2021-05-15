<template>
  <div>
    <p v-if="$fetchState.pending">Loading users...</p>
    <p v-else-if="$fetchState.error">{{ $fetchState.error.message }}</p>
    <div v-else>
      <h2>Total Results: {{ searchResults.total_count }}</h2>
      <!-- <p>{{ JSON.stringify(searchResults) }}</p> -->
      <SearchResult
        v-for="user of searchResults.items"
        :key="user.id"
        :user="user"
      />
    </div>
    <Pagination
      :page="Number(currentPage)"
      :total-results="searchResults.total_count"
      :per-page="Number(perPage)"
      :q="q"
    />
  </div>
</template>

<script>
/* eslint-disable camelcase */
export default {
  data() {
    return {
      searchResults: [],
      currentPage: this.$nuxt.context.query.page
        ? this.$nuxt.context.query.page
        : 1,
      perPage: 2,
      q: this.$nuxt.context.query.q,
    }
  },
  async fetch() {
    const defaultPostsPerPage = this.perPage || 2
    const page = this.currentPage || 1
    this.searchResults = await fetch(
      `https://api.github.com/search/users?q=${this.q}&page=${page}&per_page=${defaultPostsPerPage}`
    ).then((res) => res.json())

    if (this.searchResults.message) {
      throw new Error(
        'Github rate limiting requests. Wait a moment and try again.'
      )
    }
  },
  watch: {
    watch: { '$route.query': '$fetch' },
  },
}
</script>
