<template>
  <article>

  </article>
</template>

<script>

export default {
  async asyncData ({ app, store, params }) {
    let page = await app.$axios.get(`${store.state.wordpressAPI}`)
    store.commit('setPage', page.data[0])
  },
  computed: {
    page () {
      return this.$store.state.page
    },
  },
    head () {
      return {
        title: `${this.page.title.rendered} | ${this.$store.state.meta.name}`,
        meta: [
          { description: this.page.excerpt.rendered }
        ]
      }
    },
}
</script>
