<template>
  <div>
    <zingchart :key="random" :data="chartData"></zingchart>
  </div>
</template>

<script>
import 'zingchart/es6'
import zingchartVue from 'zingchart-vue'
import axios from 'axios'
import { map } from 'lodash'
export default {
  components: {
    zingchart: zingchartVue,
  },
  data() {
    return {
      weekdata: [],
      weeknumber : [],
      random : Math.random(),
      chartData: {
        type: 'bar',
        // scaleX: {
        //   values: [],
        //   placement: "default",
        //   tick: {
        //     size: 58,
        //     placement: "cross"
        //   }
        // },
        scaleX2: {
          values: [],
          placement: "default",
          tick: {
            size: 1,
          },
        },
        series: [
          {
            values: [],
            text: ""
          },
        ],
      },
    }
  },
  async created() {
    const data1 = await axios.get(`http://127.0.0.1:8000/api/distribution/`)
    data1.data.forEach((d) => {
      const { week_number,strain__count } = d
      this.weeknumber.push(week_number)
      this.weekdata.push(strain__count)
    })
    let s = map(data1.data, (d) => ({
        text: d.week_number,
      }))
    this.chartData.series.text = s
    this.chartData.series[0].values = this.weekdata
    this.chartData.scaleX2.values = this.weeknumber
    console.log(this.chartData.scaleX2.values)
    console.log(this.chartData.series[0].values)
    this.random = Math.random()
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
