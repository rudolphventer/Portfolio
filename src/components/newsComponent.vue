<template>
<div class="container">
    <h3>News by NewsAPI</h3>
    <br/>
  <div v-for="item in newsItems" :key="item.title">
      <div class="newsCard">
          <a v-bind:href =item.url style="text-decoration: none; color: inherit;">
              {{ item.title }}
          </a>
      </div>
  </div>
</div>
    
</template>

<script>
export default {
  name: 'NewsComponent',
  data: function () {
    return {
      newsItems: []
    }
  },
  created: async function () {
      const newsInfo = await fetch(process.env.VUE_APP_NEWS_API_URL + "top-headlines?country=us&apiKey=" + process.env.VUE_APP_NEWS_API_KEY);
        var newsJSON = await newsInfo.json();
        console.log(newsJSON.articles)
        this.newsItems = newsJSON.articles.slice(0, 5);
  }}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.newsCard{
    text-align: left;
    border: 1px rgb(105, 105, 105) none;
    border-radius: 5px;
    margin-bottom: 1rem;
    padding: 2px;
}

.newsCard:hover
{
    color: rgb(0, 122, 179);
}
</style>