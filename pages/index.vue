<template>
  <section class="container mx-auto p-4">
    <div class="px-6 py-4">
      <span v-for="source in sources" :key="source.id" class="inline-block bg-grey-lighter rounded-full mx-1 px-3 py-1 text-sm font-semibold text-grey-darker mr2">
        {{ source.name }}
      </span>
    </div>
    <div class="flex flex-col w-1/2 mx-auto">
      <div v-for="(article,index) in articles" :key="index" class="max-w-sm py-4">
        <div class="rounded overflow-hidden shadow-md">
          <a v-if="article.urlToImage !== null" :href="article.url" target="_blank">
            <img :src="article.urlToImage" :alt="article.title">
          </a>
          <div class="px-6 py-4">
            <div class="font-bold text-xl mb-2">
              <a :href="article.url" target="_blank" class="text-grey-darkest no-underline hover:text-teal">
                {{ article.title }}
              </a>
            </div>
            <p class="text-grey-darker text-base">
              {{ article.description }}
            </p>
          </div>
          <div class="px-6 py-4">
            <span class="inline-block bg-grey-lighter rounded-full px-3 py-1 text-sm font-semibold text-grey-darker mr2">
              {{ article.source.name }}
            </span>
          </div>
        </div>
      </div>
    </div>
    </div>
    <p class="text-center text-grey">
      powered by <a href="https://newsapi.org">
        NewsAPI.org
      </a>
    </p>
  </section>
</template>

<script>
// import Card from '~/components/Card.vue'

export default {
  async asyncData({ $axios }) {
    const { articles } = await $axios.$get(
      `https://newsapi.org/v2/top-headlines?country=fr&apiKey=${
        process.env.API_KEY
      }`
    )

    const { sources } = await $axios.$get(
      `https://newsapi.org/v2/sources?country=fr&apiKey=${process.env.API_KEY}`
    )
    return { articles, sources }
  }
  // components: {
  //   Card
  // }
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container-nuxt {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
