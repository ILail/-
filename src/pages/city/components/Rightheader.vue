<template>
 <ul class="list">
     <li
     class="item"
     v-for="item of letters"
     :key="item"
     :ref="item"
     @click="handleLetterClick"
     @touchstart.prevent="handTouchStart"
     @touchmove="handTouchMove"
     @touchend="handTouchEnd"
     >
     {{item}}
     </li>
 </ul>
</template>

<script>
export default{
  name: 'CityRightheader',
  props: {
    cities: Object
  },
  computed: {
    letters () {
      const letters = []
      for (let i in this.cities) {
        letters.push(i)
      }
      return letters
    }
  },
  data () {
    return {
      touchStatus: false,
      startY: 0,
      timer: null
    }
  },
  updated () {
    this.startY = this.$refs['A'][0].offsetTop
  },
  methods: {
    handleLetterClick (e) {
      this.$emit('change', e.target.innerText)
    },
    handTouchStart () {
      this.touchStatus = true
    },
    handTouchMove (e) {
      if (this.touchStatus) {
        // const startY = this.$refs["A"][0].offsetTop
        if (this.timer) {
          clearTimeout(this.timer)
        }
        this.timer = setTimeout(() => {
          const touchY = e.touches[0].clientY - 79
          const index = Math.floor((touchY - this.startY) / 20)
          if (index >= 0 && index < this.letters.length) {
            this.$emit('change', this.letters[index])
          }
        }, 16)
      }
    },
    handTouchEnd () {
      this.touchStatus = false
    }
  }
}
</script>
<!-- 1rem = html font-size = 50 px 86/100 -->
<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .list
    display flex
    flex-direction  column
    justify-content center
    position absolute
    right 0
    top 1.58rem
    bottom 0
    width .4rem
    .item
      text-align center
      line-height .4rem
      color $bgCorlor
</style>
