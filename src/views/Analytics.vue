<template>
  <div class="row">
    <div class="col s12">
      <h1>Аналитика</h1>
      <div class="chart">
        <h3>Аналитика по визитам</h3>
        <div class="chart-wrapper" ref="chartdiv"></div>
      </div>
    </div>
  </div>
</template>
<script>
import * as am4core from "@amcharts/amcharts4/core";
import * as am4charts from "@amcharts/amcharts4/charts";
import am4themes_animated from "@amcharts/amcharts4/themes/animated";

am4core.useTheme(am4themes_animated);

export default {
  mounted() {
    if (!localStorage.getItem("leadhit-site-id")) {
      this.$router.push("/");
    }
    let chart = am4core.create(this.$refs.chartdiv, am4charts.XYChart);

    chart.paddingRight = 20;

    chart.data = this.data;

    let dateAxis = chart.xAxes.push(new am4charts.DateAxis());
    dateAxis.renderer.grid.template.location = 0;

    let valueAxis = chart.yAxes.push(new am4charts.ValueAxis());
    valueAxis.renderer.minWidth = 55;

    let series = chart.series.push(new am4charts.LineSeries());
    series.dataFields.dateX = "date";
    series.dataFields.valueY = "visits";
    series.fill = am4core.color("#9500FC");
    series.fillOpacity = 0.3;
    let bullet = series.bullets.push(new am4charts.CircleBullet());
    bullet.circle.fill = am4core.color("#9500FC");
    series.strokeWidth = 3;
    series.stroke = "#9500FC";
    series.tooltipText = "{valueY}";

    chart.cursor = new am4charts.XYCursor();

    this.chart = chart;
  },
  beforeDestroy() {
    if (this.chart) {
      this.chart.dispose();
    }
  },
  computed: {
    data() {
      return this.$store.getters.data;
    },
  },
};
</script>
<style lang="scss" scoped>
.chart-wrapper {
  height: 350px;
  width: 100%;
}
</style>
