<template>
  <div id="list">
    <el-row :gutter="20" v-for="item in listData"  :to="{ path: '/' }"  tag="a">
      <el-card :body-style="{ padding: '0px' }">
        <el-col :span="8">
          <img v-bind:src="item.image_src_url" class="image">
        </el-col>
        <el-col :span="16">
          <div style="padding: 14px;">
            <span>{{item.title}}</span>
            <div class="bottom clearfix">
              <time class="time">{{item.created_at}}</time>
            </div>
          </div>
        </el-col>
      </el-card>
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
        this.tip = text
        this.getLists(text)
      })
    },
    methods: {
      getLists: function (id) {
        this.$http.post('/api/channel/' + id, {id: id}).then((response) => {
          this.listData = response.body
        })
      }
    }
  }
</script>
