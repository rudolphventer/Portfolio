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
      
        //Here I create a new array which consists of a count the occurence of each date
        var counts = {};
        eventDates.forEach(function(x) { counts[x] = (counts[x] || 0)+1; });

        //Convert int two complimentary arrays
        var dates = Object.entries(counts).map(object => moment(object[0], 'DD-MM-YYYY'))
        var occurences = Object.entries(counts).map(object => object[1])
        
        var dateArr = [];
        var occurencesArr = [];

        /* 
        Yes, this masterpiece deserves a code comment block
        Here, I create an array of the last 90 days, then check each day to see if it appears as a day where I made a commit,
        if I made a commit on that day, it increments the corresponding value in the second array by that amount.

        This seems very roundabout but graph.js requires two seperate arrays and this satisfies the constraint.
        */
        for(var i = 0; i < 90; i++)
        {
          var newDate = moment().subtract(i, "days")
          var index = dates.findIndex(function (element) { 
              return moment(newDate).isSame(moment(element, 'DD/MM/YYYY'), 'day')
          }); 
          if(index == -1)
          {
            dateArr.push(newDate.format('DD-MM-YYYY').toLocaleString());
            occurencesArr.push(0);
          } else{
            dateArr.push(newDate.format('DD-MM-YYYY').toLocaleString());
            occurencesArr.push(occurences[index]);
          }
            
        }

        
        var chartdata = {
          labels: dateArr.reverse(),
        datasets: [{
            label: 'Commits to Public Repositories in the Last 90 Days',
            data: occurencesArr.reverse(),
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
