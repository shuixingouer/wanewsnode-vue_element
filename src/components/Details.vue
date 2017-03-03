<template>
  <div class="details">
    <div class="header_tab">
      <router-link to="/"><i class="el-icon-arrow-left"></i></router-link>
    </div>
    <div class="content_des">
      <div class="des_title">
        {{detailsData[0].title}}
      </div>
      <div class="des_tip">
        <img src="./../assets/images/innerLogo.png"><span>{{detailsData[0].author}}{{detailsData[0].created_at}}</span><router-link to="/" class="into_channel">进入{{detailsData[0].channel_name}}频道</router-link>
      </div>
      <div class="des_body" v-html="detailsData[0].body">
      </div>
    </div>
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

<style lang="less">
  .details{
    overflow:hidden;
    width:100%;
    box-sizing:border-box;
    .header_tab{
      height:50px;
      line-height:50px;
      padding:0 15px;
      background:rgba(255,255,255,0.9);
      box-shadow: 0px 2px 4px 0px rgba(0, 0, 0, .12), 0px 0px 6px 0px rgba(0, 0, 0, .04);
      position:fixed;
      top:0;
      width:100%;
      box-sizing:border-box;
      a{
        color:#2c3e50;
      }
    }
    .content_des{
      margin-top:50px;
      padding:20px 15px;
      box-sizing:border-box;
      .des_title{
        font-size:22px;
        line-height:26px;
      }
      .des_tip{
        padding:10px 0 0;
        overflow:hidden;
        line-height:20px;
        font-size:13px;
        img{
          float:left;
          width:20px;
          height:20px;
          border-radius:50%;
        }
        span{
          margin-left:10px;
          float:left;
        }
        .into_channel{
          float:right;
          text-decoration:none;
          color:#00bcd4;
        }
      }
      .des_body{
        font-size:16px;
        color:#666;
        line-height:28px;
      }
    }
  }
</style>
