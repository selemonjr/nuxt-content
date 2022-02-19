<template>
<div>
    <div class="ml-5 pt-5 hover:font-bold">
       <NuxtLink to="/blog">Back To Blog</NuxtLink>
    </div>
    <article class="grid place-items-center ml-10">
      <h1 class="font-bold text-3xl mb-10 mt-3">{{article.title}}</h1>
    <nuxt-content :document="article"  class="prose prose-sm sm:prose lg:prose-lg xl:prose-2xl mx-auto"/>
</article>
</div>
</template>
<script>
export default {
    async asyncData({$content, params}) {
        const article = await $content('blog', params.slug).fetch()
        return {
            article
        }
    },
      head() {
    return {
      title: this.article.title,
      meta: [
        { hid: 'description', name: 'description', content: this.article.description },
        // Open Graph
        { hid: 'og:title', property: 'og:title', content: this.article.title },
        { hid: 'og:description', property: 'og:description', content: this.article.description },
      ]
    }
  }
}
</script>