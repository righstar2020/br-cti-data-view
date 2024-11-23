<template>
  <div id="iocs-pie-chart">
    <div class="iocs-pie-chart-title">IOCs类型分布</div>
    <dv-charts :option="option" />
  </div>
</template>

<script>
export default {
  name: 'IOCsPieChart',
  data () {
    return {
      option: {
        series: [
          {
            type: 'pie',
            radius: '50%',
            data: [
              {name: 'IP', value: 120},
              {name: '端口', value: 80}, 
              {name: 'Hash', value: 150},
              {name: 'URL', value: 100},
              {name: 'CVE', value: 90}
            ],
            insideLabel: {
              show: false
            },
            outsideLabel: {
              formatter: '{name} {percent}%',
              labelLineEndLength: 20,
              style: {
                fill: '#fff'
              },
              labelLineStyle: {
                stroke: '#fff'
              }
            }
          }
        ],
        color: ['#a1d9e8', '#52b3e1', '#008ac3', '#e86a1d', '#c33b00']
      }
    }
  },
  created() {
    this.$nextTick(() => {
      this.mockData();
      // 每30秒更新一次数据
      setInterval(() => {
        this.mockData();
      }, 30000);
    });
  },
  methods: {
    mockData() {
      const option = {
        series: [
          {
            type: 'pie',
            radius: '50%',
            data: [
              {name: 'IP', value: this.randomExtend(100, 200)},
              {name: '端口', value: this.randomExtend(50, 100)},
              {name: 'Hash', value: this.randomExtend(120, 180)},
              {name: 'URL', value: this.randomExtend(80, 150)},
              {name: 'CVE', value: this.randomExtend(60, 120)}
            ],
            insideLabel: {
              show: false
            },
            outsideLabel: {
              formatter: '{name} {percent}%',
              labelLineEndLength: 20,
              style: {
                fill: '#fff'
              },
              labelLineStyle: {
                stroke: '#fff'
              }
            }
          }
        ],
        color: ['#a1d9e8', '#52b3e1', '#008ac3', '#e86a1d', '#c33b00']
      }
      this.option = option;
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
#iocs-pie-chart {
  width: 100%;
  height: 100%;
  background-color: rgba(6, 30, 93, 0.5);
  border-top: 2px solid rgba(229, 60, 27, 0.807);
  box-sizing: border-box;

  .iocs-pie-chart-title {
    height: 50px;
    font-weight: bold;
    text-indent: 20px;
    font-size: 20px;
    font-size: 20px;
    display: flex;
    align-items: center;
  }

  .dv-charts-container {
    height: calc(~"100% - 50px");
  }
}
</style>
