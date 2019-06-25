<template>
  <aside>
    <div class="inner-container">
      <h1>Top Articles</h1>
      <article v-for="article in featuredArticles" :key="article.id">
        <nuxt-link :to="`/${article.slug}`" v-if="article._embedded['wp:featuredmedia']" class="image">
          <div class="featured lazy" v-if="featuredImage(article)">
            <div class="image-height" :style="{ paddingTop: featuredImage(article).height / featuredImage(article).width * 100 + '%' }"></div>
            <img v-lazy="featuredImage(article).source_url">
            <Spinner1/>
          </div>
        </nuxt-link>
        <div class="content">
          <div class="meta">
            <span v-html="shortTimestamp(article.date)"></span>&nbsp;–&nbsp;<nuxt-link class="topic fancy" v-for="topic in article._embedded['wp:term'][0]" :to="`/topics/${topic.slug}`" :key="topic.id" v-html="topic.name" v-if="topic.id !== $store.state.featuredID"></nuxt-link>
          </div>
          <nuxt-link :to="`/${article.slug}`" class="article">
            <h2 v-html="article.title.rendered"></h2>
            <div class="excerpt" v-html="article.excerpt.rendered"></div>
          </nuxt-link>
        </div>
      </article>
    </div>
  </aside>
</template>

<script>
import Spinner1 from '~/components/Spinner1'

export default {
  components: {
    Spinner1
  },
  props: {
    featuredArticles: Array
  },
  mixins: {
    shortTimestamp: Function
  },
  methods: {
    featuredImage (article) {
      let featuredImage = article._embedded['wp:featuredmedia']

      if (featuredImage) {
        return featuredImage[0].media_details.sizes.medium || false
      }
    }
  }
}
</script>