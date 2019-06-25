<template>
  <article>
  </article>
</template>

<script>

export default {
  async asyncData ({ app, store, params }) {
    const page = await app.$axios.get(`${store.state.wordpressAPI}/wp/v2/pages?slug=home&_embed`)
    store.commit('setPage', page.data[0])
  },
  computed: {
    page () {
      return this.$store.state.page
    },
  },
  head () {
    return {
      title: `Home | ${this.$store.state.meta.name}`,
      meta: [
        { description: this.$store.state.meta.description }
      ]
    }
  },
}
</script>
