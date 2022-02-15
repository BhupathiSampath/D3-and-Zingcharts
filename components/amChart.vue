<template>
  <div class="hello" ref="chartdiv">
  </div>
</template>
<script>
import * as am4core from "@amcharts/amcharts4/core";
import * as am4charts from "@amcharts/amcharts4/charts";
import am4themes_animated from "@amcharts/amcharts4/themes/animated";
import axios from 'axios'
am4core.useTheme(am4themes_animated);
export default {
  name: 'AmChart',
  async mounted() {
    let chart = am4core.create(this.$refs.chartdiv, am4charts.XYChart);
    chart.paddingRight = 20;
    let weeks = []
    let weekdata = []
    let data = [];
    let visits = 10;
    for (let i = 1; i < 366; i++) {
      visits += Math.round((Math.random() < 0.5 ? 1 : -1) * Math.random() * 10);
      data.push({ date: new Date(2020, 0, i),  value: visits });
    }
    // console.log(data)
    // let data1 = await axios.get(`http://127.0.0.1:8000/api/distribution/`)
    // data.push(data1.data)
    // console.log(data1.data)

    chart.data = data;
    // data1.data.forEach(d => {
    //     const {
    //         week_number,
    //         strain__count
    //     } = d;
    //     // this.state.arrWeekNumber.push(week_number)
    //     // this.state.arrweekdata.push(strain__count)
    //     chart.xAxes.push(week_number);
    //     chart.yAxes.push(strain__count);
    //     });
    // console.log(chart.xAxes)
    let dateAxis = chart.xAxes.push(new am4charts.DateAxis());
    dateAxis.renderer.grid.template.location = 0;
    let valueAxis = chart.yAxes.push(new am4charts.ValueAxis());
    valueAxis.tooltip.disabled = true;
    valueAxis.renderer.minWidth = 35;
    let series = chart.series.push(new am4charts.LineSeries());
    series.dataFields.dateX = "week_number";
    series.dataFields.valueY = "strain__count";
    series.tooltipText = "{valueY.strain__count}";
    chart.cursor = new am4charts.XYCursor();
    let scrollbarX = new am4charts.XYChartScrollbar();
    scrollbarX.series.push(series);
    chart.scrollbarX = scrollbarX;
    this.chart = chart;
  },
  beforeDestroy() {
    if (this.chart) {
      this.chart.dispose();
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  width: 100%;
  height: 500px;
}
</style>