<template>
  <div id="home" class="wrapper">
      <nav-bar  class="home-nav">
        <div slot="center">购物街</div>
      </nav-bar>
      <home-swiper :banners="banners"/>
      <recommend-view :recommends="recommends"/>
      <feature-view/>
      <tab-control :titles="['流行','新款','推荐']"></tab-control>
      <goods-list :goodslist="goods['pop'].list" />
      <ul>
        <li>li1</li>
        <li>li2</li>
        <li>li3</li>
        <li>li4</li>
        <li>li5</li>
        <li>li6</li>
        <li>li7</li>
        <li>li8</li>
        <li>li9</li>
        <li>li10</li>
      </ul>
  </div>
</template>

<script>
import HomeSwiper from './childComps/HomeSwiper'
import RecommendView from './childComps/RecommendView'
import FeatureView from './childComps/FeatureView'

import NavBar from 'components/common/navbar/NavBar'
import TabControl from "components/content/tabControl/TabControl"

import GoodsList from 'components/content/goods/GoodsList'

import { getHomeMultidata, getHomeGoods } from 'network/home.js'


export default {
  name: "Home",
  components: {
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    TabControl,
    GoodsList
  },
  data(){
    return{
      banners:[] ,
      recommends:[] ,
      goods:{
        new:{page:0 , list: []},
        pop:{page:0 , list: []},
        sell:{page:0 , list: []}
      }
    } 
  }
  ,
  created(){
    this.getHomeMultidata()
    this.getHomGoods('new',1)
    this.getHomGoods('pop',1)
    this.getHomGoods('sell',1)
    
  },
  methods:{
    getHomeMultidata(){
       getHomeMultidata()
      .then(res =>{
      this.banners = res.data.banner.list 
      this.recommends = res.data.recommend.list
    })
    },
    getHomGoods(type){
      const page = this.goods[type].page + 1
      getHomeGoods(type,page)
      .then(res =>{
        console.log(res)
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page +=1
      })
      .catch(err =>{
        console.log(err)
      })
    }
  }

};
</script>

<style scoped>
#home{
  padding-top: 44px;
  position: relative;
}
.home-nav {
    background-color: var(--color-tint);
    color: #fff;

    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 9;
}
 .tab-control {
    position: sticky;
    top: 44px;
    z-index: 10;
  }


</style>