<template>
<div class="container">
  <!-- This component takes event registration data from the API for my Conductor event booker app and displays the five most recent events -->
    <h3 class="newsCardHeading">Events from Conductor, my LAN focused event booker</h3>
    <br/>
  <div v-for="item in eventItems" :key="item._id">
      <div class="newsCard reactive">
          <a v-bind:href =url+item._id style="text-decoration: none; color: inherit;">
              <strong>{{ item.eventname }}</strong> - {{item.location}}
          </a>
      </div>
  </div>
</div>
    
</template>

<script>
export default {
  name: 'EventComponent',
  data: function () {
    return {
      eventItems: [],
      url: process.env.VUE_APP_EVENTS_FRONTEND_URL + "register/"
    }
  },
  created: async function () {
      const newsInfo = await fetch(process.env.VUE_APP_EVENTS_API_URL);
        var newsJSON = await newsInfo.json();
        this.eventItems = newsJSON.reverse().slice(0, 5);
  }}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>