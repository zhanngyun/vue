<template>
  <div id="app">
    <vHeader></vHeader>
    <div class="tab">
      <div class="tab-item border-1px">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <!-- 路由出口 -->
    <!-- 路由匹配到的组件将渲染在这里 -->
    <router-view></router-view>
  </div>
</template>

<script>
import vHeader from 'components/header/header'

const ERR_OK= 0
export default {
  name: 'App',
  data() {
    return {
      seller: {}
    }
  },
  created() {
    this.$http.jsonp('http://localhost:3000/api/seller').then((response) => {
      // get body data
      // response = response.body
      if (response.errno === ERR_OK) {
        this.seller = response.data
        console.log(this.seller)
      }
    }, response => {
      // error callback
    })
  },
  components: {
    vHeader
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin.styl"
  #app
    .tab
      display: flex
      width: 100%
      height: 40px
      line-height: 40px
      border-1px(rgba(7,17,27,0.1))
      .tab-item
        flex: 1
        text-align: center
        & > a /* &表示当前父节点 */
          display : block
          font-size: 14px
          color: rgb(77,85,93)
          &.active
            color: rgb(240,20,20)
</style>
