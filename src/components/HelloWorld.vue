<template>
  <div>
    <div :id="chartId" :style="{ width: width, height: height }"></div>
  </div>
</template>

<script>
import carbase from "../data/car.json"
export default {
  name: "MyChart",
  props: {
    chartId: {
      type: String,
      default: "asdasdas"
    },
    width: {
      type: String,
      default: "500px"
    },
    height: {
      type: String,
      default: "500px"
    },
    chartOptions: {
      type: Object

    },
    
  },
  data(){
    return {
      car:"",
      option : {
        title: {
          text: "小车走势"
        },
        tooltip: {},
        legend: {
          data: ["y轴"]
        },
        xAxis: {
          type: "category",
          data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
        },
        yAxis: {
          type: "value"
        },
        series: [
          {
            name: "价格",
            data: [220, 202, 231, 243, 225, 220, 213],
            type: "line",
            smooth: true
          }
        ]
      }
    }
  },
  mounted() {
    this.initBaseData(carbase)
    this.createChart()
  },
  methods: {
    initBaseData(base){
      console.log(base,"basedata")

      // JSON.parse((base+"")）

    },
    createChart() {
      // 基于准备好的dom，初始化echarts实例
      let chart = this.$echarts.init(document.getElementById(this.chartId));
      // 指定图表的配置项和数据
      var option = this.option
      option.xAxis.data=carbase.x  
      option.series[0].data=carbase.y
      chart.setOption(option);
    }
  }
}
</script>
