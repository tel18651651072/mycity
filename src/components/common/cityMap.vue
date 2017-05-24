<template>
    <div class="cityMap-wrapper">
        <transition name="slide-fade">

            <div class="cityMap-slider" ref="cityMapSlider" v-show="cityMapshow">
                 <input class="search" placehoder="搜索城市" v-model="city"/>
                <h4 class="cityMap-banner">热门城市</h4>
                <div class="starCity-line" v-for="(item,starCityindex) in starCity" @click="starCityClick(starCityindex)">{{item.cityName}}</div>
                <div v-for="(item,index) in alphabet" class="alphabetBlock">
                    <h4 class="cityMap-banner">{{item}}</h4>
                    <div class="starCity-line" v-if="itemData.cityFirstLetter===item" v-for="(itemData,index) in cityData" @click="itemDataClick(index)">{{itemData.cityName}}</div>
                </div>
                <div class="cityMap-navbar">
                    <ul class="cityMap-nav clearfix">
                        <li v-for="(item,index) in alphabet" @click="IndexClick(index)">
                            <h4>{{item}}</h4>
                        </li>
                    </ul>
                </div>
            </div>
        </transition>
    </div>
</template>
<script>
    import { newCity } from 'common/js/newCity'
    const alphabet = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
    export default {
        data() {
            return {
                starCity: newCity.starCity,          // 明星城市
                cityData: newCity.cityData,          // 城市数据
                alphabet: alphabet,
                city: ' '                    // 字母表
            }
        },
        computed: {
        },
        created() {

        },
        props: {
            cityMapshow: {
                type: Boolean,
                default: false
            }
        },
        watch:{
             city:function(newcity) {
                    var citytrimed = newcity.trim()
                    if (citytrimed !== ''){
                        var citycap = citytrimed.substring(0,1).toUpperCase()
                        console.log(citycap)
                        var cityIndex = alphabet.findIndex(function(el,index,arr){
                            return el===citycap;
                        })
                        console.log(cityIndex);
                        if (cityIndex){
                        this.IndexClick(cityIndex);
                        }
                    }
            }
        },
        methods: {
            // 点击字母索引到相应字母开头的城市
            IndexClick(index) {
                // console.log(index);
                var self = this
                var alphabetIndex = document.querySelectorAll('.alphabetBlock')
                self.$refs.cityMapSlider.scrollTop = alphabetIndex[index].offsetTop
                console.log(self.$refs.cityMapSlider.scrollTop)
                console.log(alphabetIndex[index].offsetTop)
            },
            // 获取明星城市的索引值
            starCityClick(starCityindex) {
                this.$emit('starCityClick', starCityindex)
            },
            // 获取城市列表的索引值
            itemDataClick(index) {
                this.$emit('itemDataClick', index)
            }
        }
    }

</script>
<style lang="stylus" rel="stylesheet/stylus">
    .cityMap-wrapper {
        .cityMap-slider {
            overflow-y: scroll;
            position: fixed;
            width: 100%;
            top: 0;
            left: 0;
            bottom:0;
            text-align: left;
            // bottom: 2rem;
            // margin-top: 2rem;
            z-index: 17;
            background: #fff;
            transition: all .6s ease-out;
            .cityMap-banner {
                background: #eee;
                padding: .05rem .5rem;
            }
            .starCity-line {
                padding: .25rem .5rem;
                border-bottom: .5px solid #ddd;
            }
            .search{
                position:fixed;
                top:0;
                width:100%;
                height:40px;
                background:orange;
            }
        }
        .cityMap-navbar {
            position: fixed;
            top: 3rem;
            right: .3rem;
            bottom: 2rem;
            overflow-y: scroll;
            z-index: 17;
            .cityMap-nav {
                padding-bottom: .6rem;
                li {
                    width: 2.6rem;
                    padding: .1rem;
                    text-align: center;
                    font-size: .56rem;
                }
            }
        }
        .slide-fade-enter-active {
            transition: all .3s ease;
        }
        .slide-fade-leave-active {
            transition: all .3s cubic-bezier(1.0, 0.5, 0.8, 1.0);
        }
        .slide-fade-enter,
        .slide-fade-leave-active {
            transform: translateX(100%);
            opacity: 1;
        }
    }
</style>