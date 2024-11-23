<template>
  <div id="attack-type-line-chart">
    <div class="dv-charts-container" id="attackTypeLineChart" style="width: 100%; height: 100%;" ></div>
  </div>
</template>

<script>
import * as echarts from "echarts";
export default {
  name: 'AttackTypeLineChart',
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
      lineChart:{},
      mockData: {
        timestamps: [],
        ddosAttacks: [],
        malware: [],
        phishing: [],
        botnet: [],
        appAttacks: []
      }
    }
  },
  watch:{
    '$store.stat.attackTypeData'(newVal,oldVal){
      if(newVal!=undefined)
        this.updateOptionData(newVal)
    }
  },
  created() {
    this.$nextTick(() => {
      this.initLineChart()
      this.generateMockData()
      this.updateOptionData(this.mockData)
      
      // 每3秒更新一次数据
      setInterval(() => {
        this.generateMockData()
        this.updateOptionData(this.mockData)
      }, 3000)
    });
  },
  methods: {
    initLineChart() {
      this.lineChart = echarts.init(document.getElementById('attackTypeLineChart'),this.darkTheme?'dark':'');
    },
    generateMockData() {
      const now = new Date()
      const timestamps = []
      const ddosAttacks = []
      const malware = []
      const phishing = []
      const botnet = []
      const appAttacks = []

      for(let i = 0; i < 10; i++) {
        timestamps.push(new Date(now - (9-i) * 3600000).toLocaleTimeString('zh-CN', {hour12: false}))
        ddosAttacks.push(this.randomExtend(50, 100))
        malware.push(this.randomExtend(30, 80))
        phishing.push(this.randomExtend(20, 60))
        botnet.push(this.randomExtend(10, 50))
        appAttacks.push(this.randomExtend(5, 40))
      }

      this.mockData = {
        timestamps,
        ddosAttacks,
        malware,
        phishing,
        botnet,
        appAttacks
      }
    },
    updateOptionData (data) {
      let option = {
        animation: this.animation,
        backgroundColor:'',
        title: {
          text: '攻击类型趋势',
          textStyle: {
            color: '#fff'
          },
          left: 15, // 使标题居中
          top: -5 // 添加top属性使标题上移
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross'
          }
        },
        legend: {
          data: ['流量攻击', '恶意软件', '钓鱼攻击', 'Botnet', '应用层攻击'],
          textStyle: {
            color: '#fff'
          },
          top: 25 // 设置legend距离顶部的距离
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          data: data.timestamps
        },
        yAxis: {
          type: 'value',
          axisLabel: {
            formatter: '{value}'
          }
        },
        series: [
          {
            name: '流量攻击',
            type: 'line',
            smooth: true,
            showSymbol: false,
            lineStyle:{
              color:'#c33b00'
            },
            data: data.ddosAttacks
          },
          {
            name: '恶意软件',
            type: 'line', 
            smooth: true,
            showSymbol: false,
            lineStyle:{
              color:'#e86a1d'
            },
            data: data.malware
          },
          {
            name: '钓鱼攻击',
            type: 'line',
            smooth: true,
            showSymbol: false,
            lineStyle:{
              color:'#008ac3'
            },
            data: data.phishing
          },
          {
            name: 'Botnet',
            type: 'line',
            smooth: true,
            showSymbol: false,
            lineStyle:{
              color:'#52b3e1'
            },
            data: data.botnet
          },
          {
            name: '应用层攻击',
            type: 'line',
            smooth: true,
            showSymbol: false,
            lineStyle:{
              color:'#a1d9e8'
            },
            data: data.appAttacks
          }
        ]
      }
      this.option = option
      this.lineChart.setOption(option)
    },
    randomExtend (minNum, maxNum) {
      if (arguments.length === 1) {
        return parseInt(Math.random() * minNum + 1, 10)
      } else {
        return parseInt(Math.random() * (maxNum - minNum + 1) + minNum, 10)
      }
    }
  }
}
</script>

<style lang="less">
#attack-type-line-chart {
  width: 100%;
  height: 100%;
  background-color: rgba(6, 30, 93, 0.5);
  border-top: 2px solid rgba(1, 153, 209, .5);
  box-sizing: border-box;

  .dv-charts-container {
    padding-top: 20px;
    height: 120%;
  }
}
</style>
