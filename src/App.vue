<template>
  <div id="app">
    <img src="./assets/logolight.png" v-show="!showPage" class="loader"/>
    <div class="Background disable-scrollbars">
    <div v-show="showPage">
      <img src="./assets/logolight.png" width="300px" height="auto">
        <div class="grid">
          <!-- The main container, much of the static data in the site is declared in the data component on this page -->
          <profile-card @clicked="waiter"/>
          <blank-component class="wide" v-html="aboutMe" />

          <git-card v-bind:repoName="greentea" @clicked="waiter"/>
          <git-card v-bind:repoName="startpage" @clicked="waiter"/>
          <git-card v-bind:repoName="portfolio" @clicked="waiter"/>

          <competence v-bind:chartdata="languageComp" v-bind:colour="0" v-bind:title='title1' class="fullwide"/>

          <event-component @clicked="waiter"/>
          <contact-me/>
          <blank-component v-html="Qualifications"/>

          <blank-component v-html="projects"/>
          <competence v-bind:chartdata="toolComp" v-bind:colour="2" v-bind:title='title2' class="wide"/>

          <stats-card class="fullwide tall"/>
          <blank-component class="fullwide" v-html="aboutPortfolio"/>
          

        </div>
    </div>
    </div>
    
  </div>
</template>

<script>
import ProfileCard from './components/profilecard.vue'
import StatsCard from './components/statscard.vue'
import GitCard from './components/gitshowcase.vue'
import BlankComponent from './components/blankComponent.vue'
import EventComponent from './components/eventComponent.vue'
import ContactMe from './components/contactMe.vue'
import competence from './components/competence.vue'

export default {
  name: 'App',
  components: {
    ProfileCard,
    StatsCard,
    GitCard,
    BlankComponent,
    EventComponent,
    ContactMe,
    competence
  },
  data() {
    return {
      readyCount : 0,
      greentea: "greentea",
      startpage: "Startpage-V2",
      portfolio: "portfolio",
      aboutMe: `<h3 style="padding-bottom: 0.5rem">About Me</h3>I am a final-year student pursuing a Bachelor of Science in Information Technology at North West University
                seeking any opportunities that allow me to gain experience in the business information technology field. I am curious
                and a tinkerer with experience in a wide range of technologies. I am a quick learner and like to teach myself new
                things and work on personal projects in my free time. I am fluent in English and Afrikaans`,
      Qualifications: 
      `<h3 class="newsCardHeading">Qualifications</h3>
      <br/>
      <div class="newsCard"><strong>National Senior Certificate (2017)</strong> Bryanston High School</div>
      <div class="newsCard"><strong>Basic Web Design course (2018)</strong> North West University</div>
      <div class="newsCard"><strong>Advanced Web Design course (2018)</strong> North West University</div>
      <div class="newsCard"><strong>BSc. IT at North West University</strong> expected graduation Dec 2020</div>
      `,
      languageComp: [
          {"name":"Javascript" , "value":80},
          {"name":"CSS/HTML" , "value":80},
          {"name":"C#" , "value":50},
          {"name":"Java" , "value":50},
          {"name":"React" , "value":40},
          {"name":"Angular" , "value":40},
          {"name":"Electron" , "value":40},
          {"name":"Vue" , "value":30},
          {"name":"Python" , "value":30},
          {"name":"C++" , "value":20 },
          {"name":"ASP.Net" , "value":20 },
          ],
      title1: 'My Experience With Languages and Frameworks',
      toolComp: [
          {"name":"Node.js/NPM" , "value": 80},
          {"name":"AWS" , "value": 60},
          {"name":"Heroku" , "value":60},
          {"name":"Github" , "value":50},
          {"name":"PWAs" , "value":50},
          {"name":"PostgreSQL" , "value":50},
          {"name":"MongoDB" , "value":45},
          {"name":"FireBase" , "value":35},
          ],
      title2: 'My Experience With Tools and Platforms',
      projects: `
      <h3 class="newsCardHeading">Projects</h3>
      <br/>
      <div class="newsCard">I am the creator of GreenTea, an open source IDE/text editor written using HTML/JS/CSS with Electron</div>
      <div class="newsCard">An event booking progressive web app called Conductor (MERN Stack)</div>
      <div class="newsCard">LAMP Stack publishing website (Similar to News24 app)</div>
      <div class="newsCard">Android chat app (Firebase + Android Studio)</div>
      <div class="newsCard">Certificate search engine for the STS association (Mendix)</div>
      <div class="newsCard">A content management web/mobile app (MEAN stack)</div>
      <div class="newsCard">CPD point accreditation and approval system (Node.js + PUG + SendGrid)</div>
      <div class="newsCard">ASP.Net Food ordering website (university project)</div>
      `,
      aboutPortfolio: 
      `
      <a style="text-decoration: none; color: inherit;" href="https://github.com/rudolphventer/Portfolio">Click here to see the ReadMe for this site. It's <strong>very</strong> entertaining</a>
      `,
      waitCounter: 0,
      waitsComplete: 0,
      showPage: false

    
    };
},
methods: {
  //Here I wait for the components to load, when they are created they emit true and when they are fully loaded they emit false, I count the true emits to see how many components
  //I am waiting for, then I wait for the amount of trues to equal the amount of falses, then I hide the spinner and show my page
    waiter (value) {
          if(value)
          {
            this.waitCounter++
          } else if(!value)
          {
            this.waitsComplete++
            if(this.waitCounter == this.waitsComplete)
            {
              this.showPage= true;
            }
          }
          //console.log("waitCounter:", this.waitCounter, "waitsComplete:", this.waitsComplete)
      },
}
}
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
