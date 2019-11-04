<template>
  <div>
    <div class="banner" @click="handleBannerClick">
      <img class="banner-img" :src="bannerImg" />
      <div class="banner-info">
        <div class="banner-title">{{ this.sightName }}</div>
        <div class="banner-number">
        <span class="iconfont banner-icon">&#xe614;</span>
          {{ this.bannerImgs.lenght }}
          </div>
      </div>
    </div>
    <!-- 公共组件画廊部分 -->
    <FadeAnimation>
    <CommonGallary :imgs="imgs" v-show="showGallary" @close="handleGrallaryClose" ></CommonGallary>
    </FadeAnimation>
    </div>
</template>

<script>
import CommonGallary from 'common/gallary/Gallary'
import FadeAnimation from 'common/fade/FadeAnimation'
export default {
  name: 'DetailBanner',
  props: {
    sightName: String,
    bannerImg: String,
    bannerImgs: Array
  },
  components: {
    CommonGallary,
    FadeAnimation
  },
  methods:{
    handleBannerClick () {
      this.showGallary = true 
    },
    handleGrallaryClose() {
      this.showGallary = false
      // 点击的时候关闭轮播图
    }
  },
  data () {
    return {
      showGallary:false,
      imgs: ["http://img1.qunarzz.com/sight/p0/1804/b6/b68ccb778c685283a3.img.jpg_r_800x800_da0c0853.jpg","http://img1.qunarzz.com/sight/p0/1804/9a/9aef54d3531b99fa3.img.jpg_r_800x800_bd66b55e.jpg"]
    }
  }
}
</script>  

<style lang="stylus" scoped>
  .banner 
    overflow hidden
    position relative
    height 0
    padding-bottom 55%
    .banner-img 
      width 100%
    .banner-info 
      display flex
      position absolute
      left  0 
      right 0 
      bottom 0
      line-height .6rem 
      color #fff
      background-image linear-gradient(top, rgba(0, 0, 0, 0) , rgba(0, 0, 0, 0.8))
      .banner-title 
        flex 1
        font-size  .32rem
        padding 0 .2rem
      .banner-number 
        height: .32rem
        line-height: .32rem
        margin-top: .14rem
        padding: 0 .4rem
        border-radius: .2rem
        background: rgba(0, 0, 0, .8)
        font-size: .24rem
        .banner-icon 
          font-size .24rem
</style>