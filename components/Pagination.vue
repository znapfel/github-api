<template>
  <div>
    <a :href="previousUrl" :aria-disabled="page <= 1">Previous</a>
    <a :href="nextUrl" :aria-disabled="page >= pageCount">Next</a>
  </div>
</template>

<script>
export default {
  props: {
    page: { type: Number, default: 1 },
    totalResults: { type: Number, default: 0 },
    q: { type: String, default: '' },
    perPage: { type: Number, default: 2 },
  },

  computed: {
    pageCount() {
      // Github API only returns 1000 results max for unauthenticated apps.
      const maxResults = this.totalResults > 1000 ? 1000 : this.totalResults
      return Math.ceil(maxResults / this.perPage)
    },
    previousUrl() {
      return `/search?q=${this.q}&page=${this.page - 1}&per_page=${
        this.perPage
      }`
    },
    nextUrl() {
      return `/search?q=${this.q}&page=${this.page + 1}&per_page=${
        this.perPage
      }`
    },
  },
}
</script>

<style>
a[aria-disabled='true'] {
  color: grey;
  pointer-events: none;
}
</style>
