<template>
  <div class="home">
    <BarChart
      class="chart"
      :key="random"
      :data-set="data"
      :margin-left="40"
      :margin-top="40"
      :tick-count="5"
      :bar-padding="0.5"
    />
  </div>
</template>

<script>
import BarChart from '@/components/D3Chart.vue'
import axios from 'axios'
export default {
  name: 'home',
  data() {
    return {
      random: Math.random(),
      data: [],
    }
  },
  components: {
    BarChart,
  },
  async created() {
    const data1 = await axios.get(`http://127.0.0.1:8000/api/d3chart/`)
    this.data = data1.data
    this.random = Math.random()
  },
}
</script>

<style scoped>
.chart {
  margin: 40px auto 0;
  display: block;
}
</style>
