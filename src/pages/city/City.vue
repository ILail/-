<template>
  <div>
    <city-lista></city-lista>
    <city-header></city-header>
    <city-search :cities="cities"></city-search>
    <city-list
    :cities="cities"
    :hot="hotCities"
    :letter="letter"
    ></city-list>
    <city-rightheader
    :cities="cities"
    @change="handeleLetterChange"
    ></city-rightheader>
  </div>
</template>

<script>
import axios from 'axios'
import CityHeader from './components/Header'
import CitySearch from './components/Search'
import CityList from './components/List'
import CityRightheader from './components/Rightheader'
import CityLista from './components/bette'
export default {
  name: 'City',
  components: {
    CityHeader,
    CitySearch,
    CityList,
    CityRightheader,
    CityLista
  },
  data () {
    return {
      cities: {},
      hotCities: [],
      letter: ''
    }
  },
  methods: {
    getCityInfo () {
      axios.get('/api/city.json')
        .then(this.handleGetCityInfoSucc)
    },
    handleGetCityInfoSucc (res) {
      console.log(res)
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.cities = data.cities
        this.hotCities = data.hotCities
      }
    },
    handeleLetterChange (letter) {
      console.log(letter)
      this.letter = letter
    }
  },
  mounted () {
    this.getCityInfo()
  }
}
</script>
<!-- 1rem = html font-size = 50 px 86/100 -->
<style lang="stylus" scoped>
</style>
