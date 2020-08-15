<template>
  <div id="home">
      <nav-bar  class="home-nav">
        <div slot="center">购物街</div>
      </nav-bar>
      <home-swiper :banners="banners"/>
      <recommend-view :recommends="recommends"/>
      <feature-view/>
      <tab-control :titles="['流行','新款','推荐']"></tab-control>
      <ul>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
      </ul>
  </div>
</template>

<script>
import HomeSwiper from './childComps/HomeSwiper'
import RecommendView from './childComps/RecommendView'
import FeatureView from './childComps/FeatureView'

import NavBar from 'components/common/navbar/NavBar'
import TabControl from "components/content/tabControl/TabControl"

import { getHomeMultidata, getHomeGoods } from 'network/home.js'


export default {
  name: "Home",
  components: {
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    TabControl
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
}
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 9;

}
</style>