<template>
 <div>
    <citySelect @cityChoice="cityChoice" :selectedCityNew="selectedCityNew"></citySelect>
      <cityMap :cityMapshow="cityMapshow" @starCityClick="starCityClick" @itemDataClick="itemDataClick"></cityMap>
 </div>
</template>
<script>
import citySelect from 'components/common/citySelect.vue'
  import cityMap from 'components/common/cityMap.vue'
  import { newCity } from 'common/js/newCity'
export default {
  name: 'mycity',
  data () {
    return {
      selectedCityNew: '请选择城市...',
      cityMapshow: false,          // 城市选择图是否显示
      starCityindex: 0,         // 明星城市index值
      itemDataindex: 0,         // 城市数据的index值
      newCity: newCity          // 城市数据
    }
  },
  methods: {
    cityChoice() {
        this.cityMapshow = true
      },
      // 明星城市选择
      starCityClick(starCityindex) {
        // console.log(this.newCity.starCity[starCityindex])
        this.cityMapshow = false
        this.selectedCityNew = this.newCity.starCity[starCityindex].cityName
        this.YourProvinceCode = this.newCity.starCity[starCityindex].provinceCode
        this.vehiclePlate = ''
      },
      // 城市选择
      itemDataClick(itemDataindex) {
        // console.log(this.newCity.cityData[itemDataindex])
        this.cityMapshow = false
        this.selectedCityNew = this.newCity.cityData[itemDataindex].cityName
        this.YourProvinceCode = this.newCity.cityData[itemDataindex].provinceCode
        this.vehiclePlate = ''
      }
  },
  components: {
    citySelect,
    cityMap
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus">

</style>
