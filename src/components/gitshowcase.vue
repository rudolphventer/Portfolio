<template>
<a v-bind:href =repo.html_url style="text-decoration: none; color: inherit;">
    <div style="display: inline-block">
        <div class="details" style="float: left">
            <h3>{{repo.name}}</h3>
            <div class="bio">{{repo.description}}</div>
            <div class="location">{{repo.full_name}}</div>
        </div>
        <doughnut v-bind:languages="languages" :maxno="totalLines" v-if="totalLines >= 0"/>
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
  data() {
    return {
      repo: {},
      languages: {},
      totalLines: Number
    }
    
  },
  created: async function () {
      const repo = await fetch("http://api.github.com/repos/rudolphventer/greentea");
        var repoData = await repo.json();
        this.repo = repoData;
        const languages = await fetch("https://api.github.com/repos/rudolphventer/greentea/languages");
        var langData = await languages.json();
        this.languages = langData;
        this.totalLines = await Object.entries(langData).reduce((a, b) => +a + +b[1], 0);
        console.log(this.totalLines)

  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped> 
.details {
    width: 50%;
}
</style>
