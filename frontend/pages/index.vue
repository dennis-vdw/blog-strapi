<template>
  <div>

    <div class="uk-section">
      <div class="uk-container uk-container-large">
        <h1>Strapi blog</h1>

        <p>{{ homepage.call_to_action }}</p>
        
        <Articles :articles="articles"></Articles>

      </div>
    </div>

  </div>
</template>

<script>
import homepageQuery from '~/apollo/queries/homepage/home'
import articlesQuery from '~/apollo/queries/article/articles'
import Articles from '~/components/Articles'

export default {
  data() {
    return {
      articles: [],
      homepage: [],
    }
  },
  components: {
    Articles
  },
  apollo: {
    articles: {
      prefetch: true,
      query: articlesQuery,
      variables () {
        return { id: parseInt(this.$route.params.id) }
      }
    },
    homepage: {
      prefetch: true,
      query: homepageQuery,
      variables () {
        return { id: parseInt(this.$route.params.id) }
      }
    }
  }
}
</script>