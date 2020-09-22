<template>
  <div id="app">
    <div class="Background disable-scrollbars">
        <img alt="Vue logo" src="./assets/logolight.png" width="300px" height="auto">
        <div class="grid">
          <profile-card/>
          <blank-component class="wide" v-html="aboutMe"/>
          
          <git-card v-bind:repoName="greentea"/>
          <git-card v-bind:repoName="startpage"/>
          <git-card v-bind:repoName="portfolio"/>
          <stats-card class="fullwide tall"/>
          <news-component/>
          <contact-me/>
          <blank-component v-html="Qualitficactions"/>
          <competence class="fullwide"/>
          

        </div>
    </div>
    
  </div>
</template>

<script>
import ProfileCard from './components/profilecard.vue'
import StatsCard from './components/statscard.vue'
import GitCard from './components/gitshowcase.vue'
import BlankComponent from './components/blankComponent.vue'
import NewsComponent from './components/newsComponent.vue'
import ContactMe from './components/contactMe.vue'
import competence from './components/competence.vue'


export default {
  name: 'App',
  components: {
    ProfileCard,
    StatsCard,
    GitCard,
    BlankComponent,
    NewsComponent,
    ContactMe,
    competence
  },
  data() {
    return {
      greentea: "greentea",
      startpage: "Startpage-V2",
      portfolio: "portfolio",
      aboutMe: `<h3 style="padding-bottom: 0.5rem">Intro to Rudolph</h3>I am a final-year student pursuing a Bachelor of Science in Information Technology at North West University
                seeking any opportunities that allow me to gain experience in the business information technology field. I am curious
                and a tinkerer with experience in a wide range of technologies. I am a quick learner and like to teach myself new
                things and work on personal projects in my free time. I am fluent in English and Afrikaans`,
      Qualitficactions: 
      `<h3 class="newsCardHeading">Qualifications</h3>
      <br/>
      <div class="newsCard"><strong>National Senior Certificate (2017)</strong> Bryanston High School</div>
      <div class="newsCard"><strong>Basic Web Design course (2018)</strong> North West University</div>
      <div class="newsCard"><strong>Advanced Web Design course (2018)</strong> North West University</div>
      <div class="newsCard"><strong>BSc. IT at North West University</strong> expected graduation Dec 2020</div>
      
      `
    
    };
}}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color:#505050 !important;
}
</style>
