<script>
import { Bar } from 'vue-chartjs'

export default {
  extends: Bar,
  props: ['chartdata', 'options', 'title', 'colour'],
  data: function () {
      return{
          count: 0
      }
      
  },
  methods: {
    //getColour returns colours in a sequence, colouring bars, there are several themes which can be specified when calling the component through the colour prop
      getColour: function () {
          var colours = [["#5e81ac", "#81a1c1", "#88c0d0", "#8fbcbb"], ["#bf616a", "#d08770", "#b48ead", "#a3be8c" ], ["#2e3440", "#3b4252", "#434c5e", "#4c566a" ], ['#6b5b95', '#feb236', '#d64161', '#5066c6', '#ff7b25', ' #b0f3ff ', ' #6380ff ', ' #413a6b ', ]]
          if(this.count < colours[this.colour].length-1)
          this.count = this.count + 1;
          else
          this.count = 0;
          return colours[this.colour][this.count];
      }
  },
  mounted: function () {
      var skills = this.chartdata
      //Supplying data to the chart
      var chartdata = {
        labels: skills.map(a => a.name),
        datasets: [{
          label: this.title,
          data: skills.map(a => a.value),
          backgroundColor: skills.map(() => {return this.getColour()}), 
        }],
     }
    var options = {
      responsive: true,
      maintainAspectRatio: false,
      scales: {
        yAxes: [{
            display: true,
            ticks: {
                suggestedMin: 0,
                suggestedMax: 100
            }
        }]
    },
    legend: {
      labels: {
   boxWidth: 0,
 }
    }
    }
    this.renderChart(chartdata, options)
  },
}
</script>

<style>
</style>
