<template>

</template>

<script>
export default {
  async asyncData ({ app, store, params }) {
    let page = await app.$axios.get(`${store.state.wordpressAPI}/wp/v2/pages?slug=${params.page}&_embed`)
    store.commit('setPage', page.data[0])
  },
  data(){
    return{
    }
  },
  components: {
  },
  computed: {
    page () {
      return this.$store.state.page
    },
  },
  mixins: {
    homeScrollTop: Function
  },
  methods: {
  },
}
</script>