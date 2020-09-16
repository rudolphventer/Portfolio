<script>
import { Line } from 'vue-chartjs'
import moment from 'moment';

export default {
  extends: Line,
  props: ['chartdata', 'options'],
  mounted: async function () {
        const events = await this.axios.get(process.env.VUE_APP_COMMITS_URL);
        //This bit of code converts the dates to a date string
        let eventDates = events.data.map(a => new Date(a.created_at.split('T')[0]).toLocaleString().split(',')[0]).reverse();
        console.log(eventDates)
      
        //Here I create a new object which ocunts the occurence of dates
        var counts = {};
        eventDates.forEach(function(x) { counts[x] = (counts[x] || 0)+1; });
        console.log(counts)

        //Convert int two complimentary arrays
        var dates = Object.entries(counts).map(object => moment(object[0], 'DD-MM-YYYY'))
        console.log(dates)
        var occurences = Object.entries(counts).map(object => object[1])
        
        var dateArr = [];
        var occurencesArr = [];
        for(var i = 0; i < 90; i++)
        {
          var newDate = moment().subtract(i, "days")
          var index = dates.findIndex(function (element) { 
              return element == newDate; 
          }); 
          if(index == -1)
          {
            dateArr.push(newDate);
            occurencesArr.push(Math.random(0,30));
          } else{
            dateArr.push(newDate);
            occurencesArr.push(occurences[index]);
          }
            
        }
        console.log(dateArr)
        console.log(occurencesArr)
        console.log(process.env.VUE_APP_USER_URL)

        
        var chartdata = {
          labels: dateArr,
        datasets: [{
            label: 'Commits to Public Repositories in the Last 90 Days',
            data: occurencesArr,
        }]}
    var options = {
      responsive: true,
      maintainAspectRatio: false
    }
    console.log(dates, occurences)
    this.renderChart(chartdata, options)
  },
}
</script>

<style>
</style>
