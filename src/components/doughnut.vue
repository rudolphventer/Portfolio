<template v-if="maxno > -1">
<!-- 
  The Doughnut component called by the gitshowcase.vue
-->
  <vc-donut
    background="white" foreground="grey"
    :size="6" unit="rem" :thickness="40"
    has-legend legend-placement="left"
    :sections="sections" :total="maxno"
    :start-angle="0" :auto-adjust-text-size="true"
    @section-click="handleSectionClick">
  </vc-donut>
</template>
<script>
  export default {
    data() {
      return {
        sections: []
      };
    },
    props: {
    languages: Object,
    maxno: Number
    },
    methods: {
      handleSectionClick(section) {
        console.log(`${section.label} clicked.`);
      },
      //This assigns colours at each call and cycles throug hthe array
      getColour(no){
        var colours = ['#6b5b95', '#feb236', '#d64161', '#5066c6', '#ff7b25', ' #b0f3ff ', ' #6380ff ', ' #413a6b ', ]
        return(colours[no]);
    }
    },
    created: async function () {
      //Getting the number of lines in the project, this allows me to work out percentages
        this.maxTotal = await this.maxno;
        var i = 0;
        for (const [key, value] of Object.entries(this.languages)) {
          this.sections.push({ label: key, value: value, color: this.getColour(i) })
          i++;
        }
    }
  };
</script>