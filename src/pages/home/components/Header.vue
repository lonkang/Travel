<template>
  <div class="header">
    <div class="header-left">
      <div class="iconfont back-icon">&#xeb99;</div>
    </div>
    <div class="header-input">
      <span class="iconfont">&#xeb9c;</span>
      输入城市/景点/游玩主题
      </div>
    <router-link to="/city">  
      <div class="header-right">
        {{this.city}}
        <span class="iconfont arrow-icon">&#xe600;</span>
      </div>
  </router-link>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  name: 'HomeHeader',
  computed: {
    ...mapState(['city'])
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .header
    display: flex
    line-height $headerHeight
    background $bgColor
    color #fff
  .header-left
    float: left
    width: .64rem
    .back-icon
      text-align center
      font-size .4rem
  .header-input
    flex: 1
    height .62rem
    line-height .62rem
    margin-top .12rem 
    margin-left .3rem 
    padding-left: .2rem
    border-radius .1rem
    background #fff
    color #ccc
  .header-right
    float right 
    min-width 1.04rem
    padding 0 .1rem
    text-align center
    color #fff
    .arrow-icon
      font-size .24rem
</style>
