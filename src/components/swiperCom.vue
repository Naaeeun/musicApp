<template>
<div id="swipercom">
    <div class="swiper-container" id="swiperIndex">
      <div class="swiper-wrapper">
          <div class="swiper-slide" v-for="(item,i) in imgs" :key="i"><img :src="item.pic"></div>
      </div>
      <!-- 如果需要分页器 -->
      <div class="swiper-pagination"></div>
    </div>
</div>
</template>

<script>
import Swiper from 'swiper'; 
import 'swiper/css/swiper.css' 
import axios from 'axios'
import {getBannner} from '@/api/index'
export default{
    data:function(){
        return{
             imgs:[
             {pic: require('../assets/img/swiper1.jpg')},
             {pic:require('../assets/img/swiper2.jpeg')},
             {pic:require('../assets/img/swiper3.jpg')}
             ]
        } 
    },
    async mounted(){
        let res = await getBannner(1)
        this.imgs = res.data.banners
        var mySwiper = new Swiper('#swiperIndex', {
            autoplay:true,
            loop: true, // 循环模式选项
        // 如果需要分页器
            pagination: {
                el: '.swiper-pagination',
                clickable:true
            },
        });   
    }
}
</script>
<style lang="less">
#swipercom{
    width: 7.5rem;
#swiperIndex.swiper-container{
    width: 7.1rem;
    height: 2.6rem;
    border-radius: 0.1rem;
    .swiper-slide img{
        width: 100%;
    }
    .swiper-pagination-bullet-active{
        background-color: orangered;
    }
}
}

</style>