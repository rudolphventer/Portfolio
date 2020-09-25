<template>
<a v-bind:href =repo.html_url style="text-decoration: none; color: inherit;">
  <!-- 
    This component recieves a repo name and gets information about that repo from the Github API, then displays
    the title and description as well as linking to the repo page. The language data is also extracted and 
    Doughnut.js is used to create a doughnut chart of the language useage. 
  -->
    <div class="cardGrid">
        <div class="detailsRepo">
            <h3>{{repo.name}}</h3>
            <div class="bio">{{repo.description}}</div>
            <div class="location">{{repo.full_name}}</div>
        </div>
        <!-- Calling my doughnut and passing props to it -->
        <doughnut class="hiddenMobile" v-bind:languages="languages" :maxno="totalLines" v-if="totalLines >= 0"/>
    </div>
</a>


</template>

<script>
import Doughnut from './doughnut.vue'
export default {
  name: 'GitCard',
  components: {
    Doughnut
  },
  props: [
    'repoName'],
  data() {
    return {
      repo: {},
      languages: {},
      totalLines: Number
    }
    
  },
  created: async function () {
        //Emitting the signal that the component has started loading
        this.sendWaiter(true);
        //Grabs repo data
        const repo = await fetch(process.env.VUE_APP_EVENTS_ROOT+this.repoName);
        var repoData = await repo.json();
        this.repo = repoData;
        //Grabs language data
        const languages = await fetch(process.env.VUE_APP_EVENTS_ROOT+this.repoName+"/languages");
        var langData = await languages.json();
        this.languages = langData;
        this.totalLines = await Object.entries(langData).reduce((a, b) => +a + +b[1], 0);
        //Emitting the signal that the component is done loading
        this.sendWaiter(false);
  },

  mounted: function () {
    console.log("mounted")
  },
  methods: {
     sendWaiter (value) {
         this.$emit('clicked', value)
     }
  }
     /*
      created: function () {
        //Emitting the signal that the component has started loading
        this.sendWaiter(true);
      },
      */
     //Emitting the signal that the component is done loading
     //this.sendWaiter(false);
  
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped> 
.details {
    width: 50%;
}
</style>
