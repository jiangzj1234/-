<template>
	<div>
	<HomeHeader ></HomeHeader>
	<HomeSwiper :list="swiperList"></HomeSwiper>
	<HomeIcons :list="iconList"></HomeIcons>
  <HomeRecommend :list="recommendList"></HomeRecommend>
  <HomeWeekend :list="weekendList"></HomeWeekend>
	</div>
</template>

<script>
	import HomeHeader from './components/Header.vue'
	import HomeSwiper from './components/Swiper.vue'
	import HomeIcons from './components/Icons.vue'
  import HomeRecommend from './components/Recommend.vue'
  import HomeWeekend from './components/Weekend.vue'
  import {mapState} from 'vuex'
  import axios from 'axios'
	export default{
		name:'Home',
		components: {
			HomeHeader,
			HomeSwiper,
			HomeIcons,
      HomeRecommend,
      HomeWeekend
		},data (){
        return {
          lastCity: '',
          swiperList:[],
          iconList:[],
          recommendList:[],
          weekendList:[]
        }
      },
      computed:{
        ...mapState(['city'])
      },
    methods:{
      getHomeInfo(){
        const recommendList = Bmob.Query("dying");
        recommendList.find().then(res => {
        this.recommendList = res;
      })
      },
    },
    mounted(){
      this.lastCity=this.city
      this.getHomeInfo()
    },
    activated (){
      if(this.lastCity !==this.city){
        this.lastCity=this.city
        this.getHomeInfo()
      }
    }
	}
</script>

<style>
	
</style>
