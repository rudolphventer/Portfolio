<template>
  <div id="app">
    <div class="Background disable-scrollbars">
        <img alt="Vue logo" src="./assets/logolight.png" width="300px" height="auto">
        <div class="grid">
          <profile-card/>
          <blank-component class="wide" v-bind:html="aboutMe"/>
          
          <git-card v-bind:repoName="greentea"/>
          <git-card v-bind:repoName="startpage"/>
          <git-card v-bind:repoName="portfolio"/>
          <stats-card class="fullwide tall"/>
          

        </div>
    </div>
    
  </div>
</template>

<script>
import ProfileCard from './components/profilecard.vue'
import StatsCard from './components/statscard.vue'
import GitCard from './components/gitshowcase.vue'
import BlankComponent from './components/blankComponent.vue'


export default {
  name: 'App',
  components: {
    ProfileCard,
    StatsCard,
    GitCard,
    BlankComponent
  },
  data() {
    return {
      greentea: "greentea",
      startpage: "Startpage-V2",
      portfolio: "portfolio",
      aboutMe: `I am a final-year student pursuing a Bachelor of Science in Information Technology at North West University
                seeking any opportunities that allow me to gain experience in the business information technology field. I am curious
                and a tinkerer with experience in a wide range of technologies. I am a quick learner and like to teach myself new
                things and work on personal projects in my free time. I am fluent in English and Afrikaans`
    
    };
}}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
