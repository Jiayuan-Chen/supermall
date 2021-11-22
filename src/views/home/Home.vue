<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <home-swiper :banners="banners"/>
    <recommend-view :recommends="recommends"/>
  </div>
</template>

<script>
import NavBar from 'components/common/navbar/NavBar';
import HomeSwiper from './childComponents/HomeSwiper';
import {getHomeMultidata} from 'network/home';
import RecommendView from './childComponents/RecommendView.vue';


  export default {
    name: "Home",
    components: {
      NavBar,
      HomeSwiper,
      RecommendView
    },
    data() {
      return {
        result: null,
        banners: [],
        recommends: []
      }
    },
    created() {
      // 1.请求多个数据
      getHomeMultidata().then(res => {
        // this.result = res;   //这里的this是外层的this，外层（created里的）this也就是整个组件的this，所以可以这么用
        this.banners = res.data.banner.list
        this.recommends = res.data.recommend.list
      }) 
    }
  }
</script>

<style scoped>
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
}
</style>
