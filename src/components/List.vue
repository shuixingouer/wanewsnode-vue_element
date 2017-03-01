<template>
  <div class="list">
    <el-row :gutter="20"  v-for="item in listData" :key="item.object_id">
      <router-link to="/details" @click="cutOff(item.object_id)">
        <el-card :body-style="{ padding:'20px 25px', overflow:'hidden' }">
          <el-col :span="7">
            <img v-bind:src="item.image_src_url" class="image">
          </el-col>
          <el-col :span="16" :offset="1">
            <div class="title">{{item.title}}</div>
            <div class="bottom clearfix">
              <time class="time">{{item.created_at}}</time>
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
        tip: '0'
      }
    },
    created () {
      bus.$on('tip', (text) => {
        this.getLists(text)
      })
    },
    methods: {
      cutOff: function (index) {
        bus.$emit('objectId', index)
        console.log(index)
      },
      getLists: function (id) {
        this.$http.post('/api/channel/' + id, {id: id}).then((response) => {
          this.listData = response.body
        })
      }
    }
  }
</script>

<style>
  .el-card{
    border:none;
  }
  .image{
    display:block;
    width:100%
  }
  .title{
    font-size:18px;
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
</style>
