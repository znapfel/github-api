<template>
  <div>
    <p v-if="$fetchState.pending">Loading users...</p>
    <p v-else-if="$fetchState.error">{{ $fetchState.error.message }}</p>
    <div v-else>
      <h2>
        <span class="total-results">{{
          new Intl.NumberFormat('en-US').format(searchResults.total_count)
        }}</span>
        Results
      </h2>
      <Pagination
        :page="Number(currentPage)"
        :total-results="searchResults.total_count"
        :per-page="Number(perPage)"
        :q="q"
      />
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
      perPage: 10,
      q: this.$nuxt.context.query.q,
    }
  },
  async fetch() {
    const headers = {
      // eslint-disable-next-line prettier/prettier
      Authorization: `${this.$config.githubToken}`,
    }
    const defaultPostsPerPage = this.perPage
    const page = this.currentPage
    this.searchResults = await fetch(
      `https://api.github.com/search/users?q=${this.q}&page=${page}&per_page=${defaultPostsPerPage}`,
      {
        headers,
      }
    ).then((res) => res.json())
  },
}
</script>

<style>
h2 {
  text-align: center;
}
.total-results {
  color: var(--accent-color);
}
</style>
