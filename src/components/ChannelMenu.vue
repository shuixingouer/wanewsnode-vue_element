<template>
  <div class="channel-menu">
    <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal" @select="handleSelect">
      <el-menu-item v-for="item in channel" :index="item.id" @click="cutOff(item.id)">{{item.channel_name}}</el-menu-item>
    </el-menu>
  </div>
</template>

<script>
import { bus } from '../bus.js'
export default {
  name: 'channelmenu',
  data () {
    return {
      activeIndex: '0',
      isActive: 0,
      channel: []
    }
  },
  created () {
    this.getLists()
  },
  methods: {
    handleSelect (key, keyPath) {
      console.log(key, keyPath)
    },
    cutOff: function (index) {
      this.isActive = index
      bus.$emit('tip', index)
    },
    getLists: function () {
      this.$http.post('/api/channel/list', {}).then((response) => {
        this.channel = response.body
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .el-menu{
    overflow:auto;
    height:50px;
    white-space:nowrap;
  }
  .el-menu--horizontal .el-menu-item{
    display:inline-block;
    float:none;
    font-size:18px;
    line-height:50px;
    height:50px;
    padding:0px 10px;
  }
</style>
