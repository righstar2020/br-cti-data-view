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
          ['DDoS,C2', '2023-10-01 05:10:45', '0x2e34...8c90'],
          ['APT29,Rootkit', '2023-10-01 04:05:33', '0x1f45...7d12'],
          ['Cryptojacking,RAT', '2023-10-01 03:15:22', '0x6b89...3e45'],
          ['Spyware,Worm', '2023-10-01 02:30:15', '0x5d34...9c78'],
          ['APT33,Keylogger', '2023-10-01 01:45:08', '0x8e12...4f56'],
          ['Adware,Virus', '2023-10-01 00:55:42', '0x2c67...8b34'],
          ['Malvertising,PUA', '2023-09-30 23:40:16', '0x7f90...1a23']
        ],
        index: true,
        columnWidth: [50, 200, 200,180],
        align: ['center'],
        rowNum: 6,
        headerBGC: '#1981f6',
        headerHeight: 45,
        oddRowBGC: 'rgba(0, 44, 81, 0.8)', 
        evenRowBGC: 'rgba(10, 29, 50, 0.8)',
        waitTime: 2000 // 添加轮播间隔时间,单位为毫秒
      }
    }
  },
  created() {
    // 每30秒更新一次数据
    setInterval(() => {
      this.mockNewData();
    }, 6000);
  },
  methods: {
    mockNewData() {
      const tags = [
        'APT41,Malware',
        'Ransomware,Botnet', 
        'Phishing,Trojan',
        'APT28,Backdoor',
        'ZeroDay,Exploit',
        'DDoS,C2',
        'APT29,Rootkit',
        'Cryptojacking,RAT',
        'Spyware,Worm',
        'APT33,Keylogger',
        'Adware,Virus',
        'Malvertising,PUA'
      ];
      
      const now = new Date();
      const hash = '0x' + Math.random().toString(16).slice(2, 10) + '...' + Math.random().toString(16).slice(2, 6);
      
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
