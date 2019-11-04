<template>
  <div>
    <CityHeader></CityHeader>
    <CitySearch :cities="cities"></CitySearch>
    <CityList 
    :hotCities="hotCities" 
    :cities="cities"
    :letter="letter"
    ></CityList>
    <CityAlphabet 
    :cities="cities"
    @change="handleLetterChange"
    ></CityAlphabet>
  </div>
</template>

<script>
import axios from 'axios'
import { mapState } from 'vuex'
import CityHeader from './components/Header'
import CitySearch from './components/Search'
import CityList from './components/List'
import CityAlphabet from './components/Alphabet'
export default {
  name: 'City',
  components:{
    CityHeader,
    CitySearch,
    CityList,
    CityAlphabet
  },
  data() {
    return {
      lastCity: '',
      hotCities: [],
      cities: {},
      letter: ''
    }
  },
    computed: {
    ...mapState(['city'])
  },
  methods:{
    getListInfo() {
      axios.get('/api/city.json?city=' + this.city).then((res) => {
        res = res.data
        if(res.ret && res.data) {
          const data = res.data
          this.hotCities = data.hotCities
          this.cities = data.cities
        }
      })
    },
    handleLetterChange (letter) {
      // 接受子组件传来的值
      this.letter = letter
    }
  },
  mounted () {
    this.lastCity = this.city
    this.getListInfo()
  },
  activated () {
    //使用了keep-live 的话 会多出这个钩子函数
    if (this.lastCity !== this.city ) {
      this.lastCity = this.city
      this.getListInfo()
    }
  }
}
</script>

<style lang="stylus" scoped>

</style>