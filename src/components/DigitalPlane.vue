<template>
  <div id="digital-flop">
    <div
      class="digital-flop-item"
      v-for="item in digitalFlopData"
      :key="item.title"
      >
      <div class="digital-flop-title">{{ item.title }}</div>
      <div class="digital-flop">
        <dv-digital-flop
          :config="item.number"
          style="width:100px;height:50px;"
           />
          <div class="unit">{{ item.unit }}</div>
      </div>
    </div>

    <dv-decoration-10 />
  </div>
</template>

<script>
import { deepCopy } from '@/util/index.js'

export default {
  name: 'DigitalPlane',
  data () {
    return {
      mockDigitalPlaneData:{
            "ctiValue":{
              'title':'情报价值',
              'number':0,
              'fill_color':'#4d99fc',
              'unit':'积分'
            },
            "ctiCount":{
              'title':'情报数量', 
              'number':0,
              'fill_color':'#f46827',
              'unit':'条'
            },
            "modelCount":{
              'title':'模型数量',
              'number':0, 
              'fill_color':'#40faee',
              'unit':'个'
            },
            "ctiTrades":{
              'title':'情报交易量',
              'number':0,
              'fill_color':'#4d99fc',
              'unit':'txs'
            },
            "modelTrades":{
              'title':'模型交易量',
              'number':0,
              'fill_color':'#4d99fc',
              'unit':'txs'
            },
            "iocsCount":{
              'title':'IOCs数量',
              'number':0,
              'fill_color':'#4d99fc',
              'unit':'个'
            },
            "userCount":{
              'title':'用户数量',
              'number':0,
              'fill_color':'#4d99fc',
              'unit':'人'
            }
      },
      digitalFlopData: [] // 添加digitalFlopData数据属性
    }
  },
  watch:{
    '$store.state.digitalPlaneData'(newVal,oldVal){
      if(newVal!=undefined){
        this.updataData(newVal)
      }
    },
  },
  created(){
    this.updataData(this.genMockDigitalPlaneData())
    setInterval(()=>{
      this.loopMockDigitalPlaneData()
    },2000)
  },
  methods: {
    loopMockDigitalPlaneData(){
      //随机一些数据
      let newMockDigitalPlaneData = this.genMockDigitalPlaneData()
      //更新数据
      this.updataData(newMockDigitalPlaneData)
  
    },
    genMockDigitalPlaneData(){
      let newMockDigitalPlaneData = this.mockDigitalPlaneData
      // 情报相关数量较大,增长也较快
      newMockDigitalPlaneData['ctiValue']['number'] = (newMockDigitalPlaneData['ctiValue']['number'] || 1000) + this.randomExtend(10,30)
      newMockDigitalPlaneData['ctiCount']['number'] = (newMockDigitalPlaneData['ctiCount']['number'] || 800) + this.randomExtend(8,20) 
      newMockDigitalPlaneData['ctiTrades']['number'] = (newMockDigitalPlaneData['ctiTrades']['number'] || 500) + this.randomExtend(5,15)
      
      // 模型相关数量中等
      newMockDigitalPlaneData['modelCount']['number'] = (newMockDigitalPlaneData['modelCount']['number'] || 200) + this.randomExtend(2,8)
      newMockDigitalPlaneData['modelTrades']['number'] = (newMockDigitalPlaneData['modelTrades']['number'] || 100) + this.randomExtend(1,5)
      
      // IOCs数量较大但增长较慢
      newMockDigitalPlaneData['iocsCount']['number'] = (newMockDigitalPlaneData['iocsCount']['number'] || 2000) + this.randomExtend(3,10)
      
      // 用户数量较少且增长最慢
      newMockDigitalPlaneData['userCount']['number'] = (newMockDigitalPlaneData['userCount']['number'] || 50) + this.randomExtend(0,2)
      
      this.mockDigitalPlaneData = newMockDigitalPlaneData
      return newMockDigitalPlaneData
    },
    updataData (digitalPlaneData) {
      let newDigitalFlopData = []
      Object.keys(digitalPlaneData).forEach((key)=>{
        newDigitalFlopData.push({
          title: digitalPlaneData[key]['title'],
          number: {
            number: [digitalPlaneData[key]['number']],
            content: '{nt}',
            textAlign: 'right',
            style: {
              fill: digitalPlaneData[key]['fill_color'],
              fontWeight: 'bold'
            }
          },
          unit: digitalPlaneData[key]['unit']
        })
      })
      this.digitalFlopData = newDigitalFlopData // 修改为digitalFlopData
    },
    randomExtend (minNum, maxNum) {
      if (arguments.length === 1) {
        return parseInt(Math.random() * minNum + 1, 10)
      } else {
        return parseInt(Math.random() * (maxNum - minNum + 1) + minNum, 10)
      }
    }

  },
  mounted () {
  }
}
</script>

<style lang="less">
#digital-flop {
  position: relative;
  height: 48%;
  margin-bottom:2%;
  flex-shrink: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: rgba(6, 30, 93, 0.5);

  .dv-decoration-10 {
    position: absolute;
    width: 95%;
    left: 2.5%;
    height: 5px;
    bottom: 0px;
  }

  .digital-flop-item {
    width: 11%;
    height: 80%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border-left: 3px solid rgb(6, 30, 93);
    border-right: 3px solid rgb(6, 30, 93);
  }

  .digital-flop-title {
    font-size: 20px;
  }

  .digital-flop {
    display: flex;
  }

  .unit {
    margin-left: 10px;
    display: flex;
    align-items: flex-end;
    box-sizing: border-box;
    padding-bottom: 13px;
  }
}
</style>
