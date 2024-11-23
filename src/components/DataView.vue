<template>
  <div class="largeScreenMonitor" >
    <dv-full-screen-container>
      <div class="header-box" >
        <TitlePlane/>
        <DigitalPlane/>
      </div>
      <div class="body-box">
          <div class="body-left-box">
              <TransactionLineChart/>
          </div>
          <div class="body-center-box">
              <IOCsWorldMap/>
          </div>
          <div class="body-right-box">
              <OnchainCtiScrollBar/>
          </div>
      </div>
      <div class="bottom-box">
        <div class="bottom-left-box">
              <AttackTypeRankingBoard/>
        </div>
          <div class="bottom-center-box">
              <AttackTypeLineChart/>
          </div>
          <div class="bottom-right-box">
              <div class="right-box-1">
                <BlockchainStatusCards/>
              </div>
              <div class="right-box-2">
                <IOCsPieChart/>
              </div>
          </div>
      </div>
    </dv-full-screen-container>
     
  </div>
</template>

<script>
import TitlePlane from './TitlePlane.vue'
import DigitalPlane from './DigitalPlane.vue'
import TransactionLineChart from './TransactionLineChart.vue'
import IOCsWorldMap from './IOCsWorldMap.vue'
import OnchainCtiScrollBar from './OnchainCtiScrollBar.vue'
import AttackTypeRankingBoard from './AttackTypeRankingBoard.vue'
import AttackTypeLineChart from './AttackTypeLineChart.vue'
import BlockchainStatusCards from './BlockchainStatusCards.vue'
import IOCsPieChart from './IOCsPieChart.vue'

export default {
  name: 'CyberGamingSimulationPage',
  components: {
    TitlePlane,
    DigitalPlane,
    TransactionLineChart,
    IOCsWorldMap,
    OnchainCtiScrollBar,
    AttackTypeRankingBoard,
    AttackTypeLineChart,
    BlockchainStatusCards,
    IOCsPieChart,
  },
  data() {
    return {
      consoleContent:[]
    }
  },
  watch:{
    '$store.state.global.message'(newVal,oldVal){
      
    }
  },
  mounted() {
  },
  created() {
    
  },
  methods: {
    
    
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
html,body{
  background-color: transparent;
  width: 100%;
  height: 100%;
  /* 禁用html的滚动条，因为用的无框架窗口，默认就会有一个滚动条，所以去掉 */
  overflow-y: hidden;
  overflow-x: hidden;
}
.largeScreenMonitor{
  width: 100%;
  height: 100%;
  background-color: #030409;
  color: #fff;
}
#dv-full-screen-container {
    height:100%;
    width: 100%;
    background-image: url('@/assets/large_screen_bg.png');
    background-size: 100% 100%;
    box-shadow: 0 0 3px blue;
    display: flex;
    flex-direction: column;
}
/*头部*/
.largeScreenMonitor .header-box{
  height: 22%;
  width: 100%;
}
/*中部*/
.largeScreenMonitor .body-box{
  height: 45%;
  width: 100%;
  display:flex;
  align-items: center;
  justify-content:flex-start;
  margin-bottom: 10px
}
.body-box .body-left-box{
  height: 100%;
  width: 29%;
  margin-right: 10px;
}
.body-box .body-center-box{
  height: 100%;
  width: 33%;
  margin-right: 10px;
}
.body-box .body-right-box{
  height: 100%;
  width: 36%;
}
/*底部*/
.largeScreenMonitor .bottom-box{
  height: 30%;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: flex-start;
}
.bottom-box .bottom-left-box{
  height: 100%;
  width: 29%;
  margin-right: 10px;
}
.bottom-box .bottom-center-box{
  height: 100%;
  width:33%;
  margin-right: 10px;
}
.bottom-box .bottom-right-box{
  height: 100%;
  width:36%;
  display: flex;
  align-items: center;
  justify-content: flex-start
}
.bottom-right-box .right-box-1{
  height: 100%;
  width: 50%;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  margin-right: 10px;
}
.bottom-right-box .right-box-2{
  height: 100%;
  width: 48%;
}
</style>
