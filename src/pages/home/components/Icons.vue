<template>
  <div class="icons">
  <swiper :options="swiperOption">
    <!-- 把pages中所有的页面循环显示出来 -->
      <swiper-slide v-for="(page, index) of pages" :key="index">
        <!-- 把每一个页面中的图标循环渲染出来 -->
        <div class="icon"
        v-for="item of page"
        :key = item.id
        >
          <div class="icon-img">
            <img class="icon-img-content" :src="item.imgUrl" />
          </div>
          <p class="icon-desc">{{ item.desc }}</p>
        </div>
      </swiper-slide>
  </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeIcons',
  data() {
    return{
      swiperOption: {
        autoPlay: false
      }
    }
  },
  props: {
    list: Array
  },
  computed: {
    pages () {
      const pages = []
      this.list.forEach((item, index) => {
        // 判断有几页
        const page = Math.floor(index/8)
        // 如果pages中的page没有数据就定义为空
        if(!pages[page]){
          pages[page] = []
        }
        // 把第二页的图标放在第二页中
        pages[page].push(item)
      })
      return pages
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  @import '~styles/mixins.styl'
  .icons >>> .swiper-container
    height: 0
    padding-bottom: 50%
  .icons
    margin-top: .1rem
    .icon
      position: relative
      overflow: hidden
      float: left
      width: 25%
      height: 0
      padding-bottom: 25%
      .icon-img
        position: absolute
        top: 0
        left: 0
        right: 0
        bottom: .44rem
        box-sizing: border-box
        padding: .1rem
        .icon-img-content
          display: block
          margin: 0 auto
          height: 100%
      .icon-desc
        position: absolute
        left: 0
        right: 0
        bottom: 0
        height: .44rem
        line-height: .44rem
        text-align: center
        color: $darkTextColor
        ellipsis()
</style>
