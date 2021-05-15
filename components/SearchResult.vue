<template>
  <pre>{{ user }}</pre>
</template>

<script>
export default {
  props: {
    user: {
      type: Object,
      default() {
        return {}
      },
    },
  },
}
</script>
