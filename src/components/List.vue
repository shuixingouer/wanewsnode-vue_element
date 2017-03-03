<template>
  <div class="list">
    <el-row :gutter="20"  v-for="item in listData" :key="item.object_id">
      <router-link :to="{ path: '/details?id='+ item.object_id }">
        <el-card :body-style="{ margin:'20px 25px',padding:'0', overflow:'hidden', position:'relative' }">
          <el-col :span="7">
            <div class="image" :style="{ width:width }" ref="wHeight">
              <img v-lazy="item.image_src_url" class="image1">
              <div class="image2" :style="{ backgroundImage:'url('+item.image_src_url+')' }"></div>
            </div>
          </el-col>
          <el-col :span="16" :offset="1">
            <div class="title">{{item.title}}</div>
            <div class="bottom clearfix">
              <div class="time">{{item.created_at}}</div>
            </div>
          </el-col>
        </el-card>
      </router-link>
    </el-row>
  </div>
</template>

<script>
  import { bus } from '../bus.js'
  export default {
    name: 'list',
    data () {
      return {
        listData: [],
        tip: '1',
        width: '100%'
      }
    },
    created () {
      this.getLists(1)
      bus.$on('tip', (text) => {
        this.getLists(text)
      })
      this.WidthHeightCalculation()
    },
    methods: {
      getLists: function (id) {
        this.$http.post('/api/channel/' + id, {id: id}).then((response) => {
          this.listData = response.body
        })
      },
      WidthHeightCalculation: function () {
        this.$refs.wHeight.style.height=document.getElementsByClassName('image').clientWidth * 9 / 16
      }
    }
  }
</script>

<style lang="less">
  .list{
    margin-top:100px;
    box-sizing:border-box;
    overflow:hidden;
    width:100%;
  .el-card{
    border:none;
  }
  .image{
    display:block;
    position:relative;
    background:#efefef;
  }
  .image1{
    position:absolute;
    width:100%;
    height:100%;
    top:0;
    left:0;
  }
  .image2{
    position:absolute;
    top:0;
    left:0;
    width:100%;
    height:100%;
    background-size:cover;
    background-repeat:no-repeat;
    background-position:top left;
  }
  .title{
    font-size:16px;
    color:#000;
    line-height:24px;
    height:48px;
    text-overflow:-o-ellipsis-lastline;
    overflow:hidden;
    text-overflow:ellipsis;
    display:-webkit-box;
    -webkit-line-clamp:2;
    -webkit-box-orient:vertical
  }
  .bottom{
    position:absolute;
    bottom:0;
    right:0;
  }
  .time{
    color:#999;
    font-size:12px;
  }
  }
</style>
