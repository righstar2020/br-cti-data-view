<template>
  <div id="transaction-line-chart">
    <div class="dv-charts-container" id="transactionLineChart" style="width: 100%; height: 100%;" ></div>
  </div>
</template>

<script>
import * as echarts from "echarts";
export default {
  name: 'TransactionLineChart',
  props: { 
    animation:{
      type:Boolean,
      default:true
    },
    darkTheme:{
      type:Boolean,
      default:true
    },
  },
  data () {
    return {
      option: {},
      mockData: {
        timestamps: [],
        ctiTrades: [],
        modelTrades: []
      }
    }
  },
  created() {
    this.$nextTick(() => {
      this.initLineChart()
      this.generateMockData()
      this.startMockDataUpdate()
    });
  },
  methods: {
    initLineChart() {
      this.lineChart = echarts.init(document.getElementById('transactionLineChart'),this.darkTheme?'dark':'');
    },
    generateMockData() {
      // 生成最近24小时的时间戳
      const now = new Date()
      for(let i = 23; i >= 0; i--) {
        const time = new Date(now - i * 3600 * 1000)
        this.mockData.timestamps.push(time.toLocaleTimeString())
        this.mockData.ctiTrades.push(Math.floor(Math.random() * 100))
        this.mockData.modelTrades.push(Math.floor(Math.random() * 50))
      }
      this.updateChart()
    },
    startMockDataUpdate() {
      setInterval(() => {
        // 移除最早的数据点
        this.mockData.timestamps.shift()
        this.mockData.ctiTrades.shift()
        this.mockData.modelTrades.shift()
        
        // 添加新的数据点
        const now = new Date()
        this.mockData.timestamps.push(now.toLocaleTimeString())
        this.mockData.ctiTrades.push(Math.floor(Math.random() * 100))
        this.mockData.modelTrades.push(Math.floor(Math.random() * 50))
        
        this.updateChart()
      }, 3000)
    },
    updateChart() {
      this.option = {
        animation: this.animation,
        backgroundColor:'transparent',
        grid:{
          left: '3%',
          right: '4%',
          bottom: '10%',
          top: '20%',
          containLabel: true
        },
        title: {
          text: '交易趋势监控',
          subtext: '情报交易量/模型交易量'
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross'
          }
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          data: this.mockData.timestamps
        },
        yAxis: {
          type: 'value',
          axisLine: {
            show: true,
            lineStyle: {
              color: 'black',
              width: 1,
              type: 'solid'
            }
          },
          axisLabel: {
            formatter: '{value} txs'
          }
        },
        legend: {
          data: ['情报交易量', '模型交易量']
        },
        series: [
          {
            name: '情报交易量',
            type: 'line',
            smooth: true,
            showSymbol: false,
            lineStyle:{
              color:'rgba(57, 134, 215, 0.807)'
            },
            areaStyle: {
              color:'rgba(57, 134, 215, 0.807)'
            },
            data: this.mockData.ctiTrades
          },
          {
            name: '模型交易量',
            type: 'line',
            smooth: true,
            showSymbol: false,
            lineStyle:{
              color:'rgba(230, 162, 60, 0.807)'
            },
            areaStyle: {
              color:'rgba(230, 162, 60, 0.807)'
            },
            data: this.mockData.modelTrades
          }
        ]
      }
      if(this.lineChart!=null)
        this.lineChart.setOption(this.option,true)
    }
  },
  mounted () {
  }
}
</script>

<style lang="less">
#transaction-line-chart {
  width: 100%;
  height: 100%;
  background-color: rgba(6, 30, 93, 0.5);
  border-top: 2px solid rgba(1, 153, 209, .5);
  box-sizing: border-box;
  margin-right: 10px;

  .dv-charts-container {
    margin-top: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
  }
}
</style>
