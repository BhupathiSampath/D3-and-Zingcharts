<template>
<dir>
  <d-3-barchart/>
  <am-chart />
  <Zingchart />
</dir>
</template>

<script>
import AmChart from '@/components/amChart.vue'
import D3Barchart from '@/components/D3Barchart.vue'
import Zingchart from '@/components/Zingchart.vue'
export default {
  components: { D3Barchart, AmChart, Zingchart},
  name: 'IndexPage'
}
</script>
