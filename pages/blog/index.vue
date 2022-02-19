<template>
<div>
  <section class="text-gray-600 body-font overflow-hidden">
    <div class="grid place-items-center">
        <h1 class="font-bold text-3xl mt-2">Nuxt Content</h1>
    </div>
  <div v-for="article in articles" :key="article.id" class="container px-5 py-24 mx-auto">
    <div class="-my-20 divide-y-2 divide-gray-100">
      <div class="py-8 flex flex-wrap md:flex-nowrap">
        <div class="md:w-64 md:mb-0 mb-6 flex-shrink-0 flex flex-col">
          <span class="font-semibold title-font text-gray-700">CATEGORY</span>
          <span class="mt-1 text-gray-500 text-sm">{{article.createdAt | formatDate}}</span>
        </div>
        <div class="md:flex-grow">
          <img :src="article.img" :alt="article.title" class="w-96 h-64 rounded-md mb-3">
          <h2 class="text-2xl font-medium text-gray-900 title-font mb-2">{{article.title}}</h2>
          <p class="leading-relaxed">{{article.description}}</p>
          <a class="text-indigo-500 inline-flex items-center mt-4"><nuxt-link :to="`/blog/${article.slug}/`">Learn More</nuxt-link>
          </a>
        </div>
      </div>
      </div>
      </div>
    </section>
</div>
</template>

<script>
import {format} from 'date-fns'
export default {
  name:"BlogPage",
  filters: {
    formatDate () {
      return format(new Date(), 'dd MMM yyyy')
    }
  },
  async asyncData(context) {
    const {$content} = context
    const articles = await $content('blog').fetch();
    return {
      articles
    }
}
}
</script>
