<template>
  <div class="grid">
    <h1>Noticias: {{ q }}</h1>
    <div v-for="(n, index) in news" :key="index" class="item">
      <div class="image">
        <img :src="n.urlToImage" alt="">
      </div>
      <h2>{{ n.title }}</h2>
      <summary>
        <p>{{ n.description }}</p>
      </summary>
      <div class="link">
        <a :href="n.url" target="_blank">Leer más</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NewsIndex',

  async asyncData({ $axios, params, $config }) {
    const { data } = await $axios.get(`https://newsapi.org/v2/everything?q=${params.q}&apiKey=${$config.newsApiKey}`)
    return {
      news: data.articles,
      q: params.q
    }
  },
}
</script>

<style>
  body {
    background: #fafafa;
    padding: 2em;
  }

  .grid {
    display: flex;
    flex-direction: column;
    gap: 2em;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  h1 {
    color: #333;
  }

  .item {
    border: 1px solid #eee;
    padding: 1em;
    border-radius: 1em;
  }

  .item:hover {
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }

  .image {
    text-align: center;
  }

  img {
    max-width: 100%;
  }

  .link {
    text-align: right;
  }

  a {
    color: #3f3f3f;
  }
</style>
