<template>
<div class="app-container">
  <div>
      <v-header :seller='seller'></v-header>
      <div class="tab border-1px">
        <div class="tab-item">
          <router-link to="/goods">商品</router-link>
        </div>
        <div class="tab-item">
          <router-link to="/ratings">评论</router-link>
        </div>
        <div class="tab-item">
          <router-link to="/seller">商家</router-link></div>
        </div>
      </div>
      <router-view :seller="seller"></router-view>
  </div>
</div>
</template>

<script  type="text/ecmascript-6">
  import header from './components/header/header.vue';
  const ERR_OK = 0;
  export default{
    data () {
      return {
        seller: {}
      };
    },
    created () {
      this.$http.get('/api/seller').then((response) => {
        response = response.body;
        console.log(response);
        if (response.errno === ERR_OK) {
          this.seller = response.data;
          console.log(this.seller);
        }
      });
    },
    components: {
      'v-header': header
    }
  };
  
</script>

<style lang="stylus" type="text/stylus" rel="stylesheet/stylus">
    @import './common/stylus/index.styl';
    .tab
      display:flex
      width:100%
      height:40px
      line-height 40px
      border-1px(rgba(0,7,17,.5))
      .tab-item
        flex:1
        text-align center
</style>
