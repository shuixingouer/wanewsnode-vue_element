<template>
  <div class="details">
    <el-row :gutter="20">
      {{item.body}}
    </el-row>
  </div>
</template>

<script>
  import { bus } from '../bus.js'
  export default {
    name: 'details',
    data () {
      return {
        detailsData: [],
        objectId: '0'
      }
    },
    created () {
      this.getDetails(0)
      bus.$on('objectId', (text) => {
        this.getDetails(text)
      })
    },
    methods: {
      getDetails: function (id) {
        this.$http.post('/api/static/detail/' + id, {id: id}).then((response) => {
          this.detailsData = response.body
          console.log(response)
        })
      }
    }
  }
</script>

<style>

</style>
