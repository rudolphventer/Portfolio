<template>
  <div id="app">
    <div class="Background disable-scrollbars">
        <img alt="Vue logo" src="./assets/logolight.png" width="300px" height="auto">
        <div class="grid">
          <profile-card/>
          <stats-card/>

        </div>
    </div>
    
  </div>
</template>

<script>
import ProfileCard from './components/profilecard.vue'
import StatsCard from './components/statscard.vue'

export default {
  name: 'App',
  components: {
    ProfileCard,
    StatsCard
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
