<template>
    <div class="list" ref="wrapper">
        <div>
            <div class="area">
                <div class="title border-topbottom">当前城市</div>
                <div class="button-list">
                    <div class="button-wrapper">
                        <div class="button">{{this.$store.state.city}}</div>
                    </div>
                </div>
            </div>
            <div class="area">
                <div class="title border-topbottom">热门城市</div>
                <div class="button-list">
                    <div class="button-wrapper" v-for= "item of hot" :key="item.id" @click="handleCityClick(item.name)">
                        <div class="button">{{item.name}}</div>
                    </div>
                </div>
            </div>
            <div class="area"
            v-for="(item , key) of cities"
            :key = "key"
            :ref = "key"
            >
            <div class="title border-topbottom">{{key}}</div>
                <div class="item-list">
                    <div class="item border-bottom"
                         v-for="innnerItem of item"
                         :key = "innnerItem.id"
                         @click="handleCityClick(innnerItem.name)"
                    >
                      {{innnerItem.name}}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Bscroll from 'better-scroll'
export default{
  name: 'CityHeader',
  props: {
    hot: Array,
    cities: Object,
    letter: String
  },
  methods: {
    handleCityClick (city) {
      this.$store.commit('changeCity', city)
      this.$router.push('/')
    }
  },
  watch: {
    letter () {
      if (this.letter) {
        const ele = this.$refs[this.letter][0]
        this.scroll.scrollToElement(ele)
      }
    }
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.wrapper)
  }
}
</script>
<!-- 1rem = html font-size = 50 px 86/100 -->
<style lang="stylus" scoped>
@import '~styles/varibles.styl';
.list{
    overflow hidden
    position absolute
    top 1.58rem
    left 0
    right 0
    bottom 0
}
.border-topbottom {
    &:before {
        border-color: #ccc;
    }

    &:after {
        border-color: #ccc;
    }
}

.border-bottom {
    &:before {
        border-color: #ccc;
    }
}
.title {
    line-height: 0.54rem;
    background: #eee;
    padding-left: 0.2rem;
    color: #666;
    font-size: 0.26rem;
}

.button-list {
    overflow: hidden;
    padding: 0.1rem .6rem .1rem .1rem;

    .button-wrapper {
        float: left;
        width: 33.33%;

        .button {
            margin: 0.1rem;
            padding: 0.1rem 0;
            text-align: center;
            border: 0.02rem solid #ccc;
            border-radius .06rem;
        }
    }
}
.item-list{
    .item{
        line-height .76rem
        padding-left .2rem
    }
}
</style>
