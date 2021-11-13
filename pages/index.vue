<template>
  <div>
    <h1>Trying things</h1>
    <div v-for="article in articles" :key="article.id">
      {{ article.slug }}
      {{ article.createdAt | formatDate }}
      {{ article.description }}
    </div>
  </div>
</template>

<script>
import { format } from 'date-fns'
export default {
  name: 'Blog',
  filters: {
    formatDate() {
      return format(new Date(), 'dd MMM yyyy')
    },
  },
  async asyncData(context) {
    const { $content } = context
    const articles = await $content('blog').fetch()
    console.log(articles)
    return { articles }
  },
}
</script>
