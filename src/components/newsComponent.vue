<template>
<div class="container">
    <h3 class="newsCardHeading">Events from Conductor, my LAN focused event booker</h3>
    <br/>
  <div v-for="item in newsItems" :key="item._id">
      <div class="newsCard">
          <a v-bind:href =url+item._id style="text-decoration: none; color: inherit;">
              <strong>{{ item.eventname }}</strong> - {{item.location}}
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
      newsItems: [],
      url: process.env.VUE_APP_EVENTS_FRONTEND_URL + "register/"
    }
  },
  created: async function () {
      const newsInfo = await fetch(process.env.VUE_APP_EVENTS_API_URL);
        var newsJSON = await newsInfo.json();
        console.log(newsJSON)
        this.newsItems = newsJSON.reverse().slice(0, 5);
  }}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>