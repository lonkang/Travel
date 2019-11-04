<template>
  <ul class="list" >
      <li
      class="item"
      v-for="item of letters"
      :key="item"
      :ref="item"
      @touchstart.prevent="handleTouchStart"
      @touchmove="handleTouchMove"
      @touchend="handleTouchEnd"
      @click="handleLetterClick"
      >
      {{ item }}
      </li>
  </ul>
  <!-- 移动端有Touch事件 -->
</template>

<script>
export default {
  name: 'CityAphlphabet',
  props: {
    cities: Object
  },
  data() {
    return {
      touchStatus: false,
      startY: 0,
      timer: null
    }
  },
  computed: {
    letters () {
      const letters = []
      for (let i in this.cities) {
        letters.push(i)
      }
      // 通过计算属性把cities中的字母循环渲染为一个数组
      return letters
    }
  },
  updated () {
    // 获取A距离顶部的值
    // 数据更新的时候调用
    this.startY = this.$refs['A'][0].offsetTop
  },
  methods: {
    handleLetterClick(e) {
      // 点击的时候会有一个e的参数可以获取被点击的内容
      // console.log(e.target.innerText)
      // 子向父传值
      this.$emit('change', e.target.innerText)
    },
    handleTouchStart() {
      // 手指点击开始的位置
      this.touchStatus = true
    },
    handleTouchMove (e) {
      // 移动过程中有个e的参数可以获取到移动的元素
      //获取A元素距离top的位置  再获取 当前元素距离顶部的位置 
      // 两个的差值再除以每一个字母的高度就可以知道是第几个字母了 
      // 然后触发一个Change事件给外部就可以了
      // 手指移动的时候 位置一个变
      if (this.touchStatus) {
        //获取当前字母距离顶部的值
        // 随着手指的移动 e中有个touches的数组 第0项就是当前dom元素
        // 79是header和input框的值
        if(this.timer) {
          clearTimeout(this.timer)
        }
        // 默认的move事件 移动速度很快 所以 我们做一个数据截留 
        // 当在10毫秒内同时点击的是一个元素 我们停止上一次的点击
        // 也就是在10毫秒内点击同一元素只会触发一次
        this.timer = setTimeout( () => {
        const touchY = e.touches[0].clientY - 79
        // 获取到要移动的下标
        const index = Math.floor((touchY - this.startY) / 20)
        if (index >= 0 && index < this.letters.length) {
          this.$emit('change', this.letters[index])
        }
        }, 10)
        
      }
    },
    handleTouchEnd() {
      // 手指停下的时候
      this.touchStatus = false
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl';
  .list
    display flex
    flex-direction column
    justify-content center
    position absolute 
    top 1.58rem
    right 0
    bottom 0
    width .4rem
    .item 
      line-height .4rem
      text-align center
      color  $bgColor
</style>