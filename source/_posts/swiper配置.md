title: swiper配置
author: 大白腿
tags:
  - swiper
  - js
  - ''
categories:
  - js
date: 2020-05-24 12:44:00
---
```js
     slidesPerColumnFill : 'row' //表格swiper横着排
      centeredSlides: true //选中居中
      breakpoints: {
        767: {
          slidesPerView: 2,
        },
		}
```
解决tab bug
```js
     observer:true,//修改swiper自己或子元素时，自动初始化swiper
      	observeParents:true,
      	loopFillGroupWithBlank: true,
     }
```