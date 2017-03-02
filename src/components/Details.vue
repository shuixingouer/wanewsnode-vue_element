<template>
  <div class="details">
    <el-row :gutter="20">
      {{ detailsData[0].body }}
    </el-row>
  </div>
</template>

<script>
  export default {
    name: 'details',
    data () {
      return {
        detailsData: []
      }
    },
    created () {
      console.log(this.$route.query.id)
      this.getDetails(this.$route.query.id)
    },
    methods: {
      getDetails: function (id) {
        console.log(id)
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
