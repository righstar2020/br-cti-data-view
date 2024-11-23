<template>
  <div id="scroll-board">
    <dv-scroll-board :config="option" />
  </div>
</template>

<script>
import {deepCopy} from "@/util/index.js";
export default {
  name: 'OnchainCtiScrollBoard',
  data () {
    return {
      option: {
        header: ['Tags', '时间', '链上Hash'],
        data: [
          ['APT41,Malware', '2023-10-01 10:23:45', '0x8f23...4d21'],
          ['Ransomware,Botnet', '2023-10-01 09:15:32', '0x7a12...9f34'],
          ['Phishing,Trojan', '2023-10-01 08:45:12', '0x3b45...2e67'],
          ['APT28,Backdoor', '2023-10-01 07:30:25', '0x9c56...1a89'],
          ['ZeroDay,Exploit', '2023-10-01 06:20:18', '0x4d78...5b23'],
          ['DDoS,C2', '2023-10-01 05:10:45', '0x2e34...8c90']
        ],
        index: true,
        columnWidth: [50, 200, 200,180],
        align: ['center'],
        rowNum: 6,
        headerBGC: '#1981f6',
        headerHeight: 45,
        oddRowBGC: 'rgba(0, 44, 81, 0.8)', 
        evenRowBGC: 'rgba(10, 29, 50, 0.8)'
      }
    }
  },
  created() {
    // 每30秒更新一次数据
    setInterval(() => {
      this.mockNewData();
    }, 30000);
  },
  methods: {
    mockNewData() {
      const tags = [
        'APT41,Malware',
        'Ransomware,Botnet', 
        'Phishing,Trojan',
        'APT28,Backdoor',
        'ZeroDay,Exploit',
        'DDoS,C2'
      ];
      
      const now = new Date();
      const hash = '0x' + Math.random().toString(16).substr(2, 8) + '...' + Math.random().toString(16).substr(2, 4);
      
      const newData = [
        tags[Math.floor(Math.random() * tags.length)],
        now.toLocaleString(),
        hash
      ];
      
      let currentData = this.option.data;
      currentData.unshift(newData);
      currentData = currentData.slice(0, 6);
      
      this.option = {
        ...this.option,
        data: currentData
      };
    }
  }
}
</script>

<style lang="less">
#scroll-board {
  width: 100%;
  box-sizing: border-box;
  height: 100%;
  overflow: hidden;
  .dv-scroll-board{
    height: 100%;
    width: 100%;
  }
}
</style>
