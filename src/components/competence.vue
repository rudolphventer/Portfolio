<script>
import { Bar } from 'vue-chartjs'

export default {
  extends: Bar,
  props: ['chartdata', 'options'],
  data: function () {
      return{
          count: 0
      }
      
  },
  methods: {
      getColour: function () {
          var colours = ["#5e81ac", "#81a1c1", "#88c0d0", "#8fbcbb"]
          if(this.count < colours.length-1)
          this.count = this.count + 1;
          else
          this.count = 0;
          return colours[this.count];
      }
  },
  mounted: async function () {
      var skills = [
          {"name":"Javascript" , "value":50, "colour": this.getColour() },
          {"name":"CSS/HTML" , "value":50, "colour": this.getColour() },
          {"name":"React" , "value":40, "colour": this.getColour() },
          {"name":"Angular" , "value":40, "colour": this.getColour() },
          {"name":"Vue" , "value":30, "colour": this.getColour() },
          {"name":"C#" , "value":40, "colour": this.getColour() },
          {"name":"Python" , "value":30, "colour": this.getColour() },
          {"name":"C++" , "value":20, "colour": this.getColour() },
          {"name":".Net" , "value":20, "colour": this.getColour() },
          ]
        var chartdata = {
          labels: skills.map(a => a.name),
        datasets: [{
            label: 'My Skills',
            data: skills.map(a => a.value),
            backgroundColor: skills.map(a => a.colour), 
            
        }]}
    var options = {
      responsive: true,
      maintainAspectRatio: false
    }
    this.renderChart(chartdata, options)
  },
}
</script>

<style>
</style>
