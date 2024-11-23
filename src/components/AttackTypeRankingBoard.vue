<template>
  <div id="attack-type-ranking-board">
    <div class="attack-type-ranking-board-title">攻击类型排行</div>
    <dv-scroll-ranking-board :config="option" />
  </div>
</template>

<script>
import {deepCopy} from "@/util/index.js";
export default {
  name: 'AttackTypeRankingBoard',
  data () {
    return {
      option: {
        data: [
          {
            name: '流量攻击',
            value: 892
          },
          {
            name: '恶意软件',
            value: 756
          },
          {
            name: '钓鱼攻击', 
            value: 634
          },
          {
            name: 'Botnet',
            value: 521
          },
          {
            name: '应用层攻击',
            value: 423
          }
        ],
        rowNum: 5
      }
    }
  },
  watch:{
    '$store.state.threatIntel.attackTypeRankData'(newVal,oldVal){
      if(newVal!=undefined){
        this.updateOptionData(newVal)
      }
    }
  },
  created() {
    this.$nextTick(() => {
      let attackTypeRankData = this.$store.getters.getThreatIntelData['attackTypeRankData']
      if(attackTypeRankData!=undefined)
          this.updateOptionData(attackTypeRankData)
    });
  },
  methods: {
    updateOptionData(attackTypeRankData){
      if(!attackTypeRankData || Object.values(attackTypeRankData).length === 0){
        return
      }
      
      this.option = {
        data: Object.entries(attackTypeRankData).map(([name, value]) => ({
          name,
          value
        })),
        rowNum: 5
      }
    }
  }
}
</script>

<style lang="less">
#attack-type-ranking-board {
  width: 100%;
  height: 100%;
  box-shadow: 0 0 3px blue;
  display: flex;
  flex-direction: column;
  background-color: rgba(6, 30, 93, 0.5);
  border-top: 2px solid rgba(1, 153, 209, .5);
  box-sizing: border-box;
  padding: 0px 30px;

  .attack-type-ranking-board-title {
    font-weight: bold;
    height: 50px;
    display: flex;
    align-items: center;
    font-size: 20px;
  }

  .dv-scroll-ranking-board {
    flex: 1;
    height: 90%;
  }
}
</style>
