title: vue使用swiper
author: 大白腿
tags:
  - swiper
  - vue
categories:
  - vue
date: 2020-05-24 15:16:00
---
//安装swiper
第一步: 安装  npm i vue-awesome-swiper --save( 这一个是否安装根据实际情况,如果安装上一个你用没效果也要安装这个 =>  npm i swiper )


第二步: 在main.js文件里引入

```js
import VueAwesomeSwiper from 'vue-awesome-swiper'
import 'swiper/css/swiper.css'
Vue.use(VueAwesomeSwiper)
```

 

第三步;

```html
<swiper :options="swiperOption">
　　<swiper-slide v-for="items in allData.bannerphoto" key="items">
　　　　<img :src="items" alt="">
　　</swiper-slide>
　　<div class="swiper-pagination" slot="pagination"></div> (分页器)
</swiper>
```


 
在data里定义轮播图
```js
swiperOption: {
　　pagination: '.swiper-pagination',
　　paginationClickable: true,
　　autoplay: 2500,
　　autoplayDisableOnInteraction: false,
　　loop: false,
　　coverflow: {(轮播图切换方式)
　　　　rotate: 30,
　　　　stretch: 10,
　　　　depth: 60,
　　　　modifier: 2,
　　　　slideShadows : true
　　}
},
```
