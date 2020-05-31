title: vue点击回顶部
author: 大白腿
tags:
  - vue
categories:
  - vue
date: 2020-05-24 15:10:00
---
//同页面点击瞬间回到顶部
 ```js
   document.body.scrollTop = document.documentElement.scrollTop = 0;
 ```
//点击路由回到顶部(瞬间) 
main.js里
```
router.afterEach((to,from,next) => {
  window.scrollTo(0,0);
})
```

//回到顶部(有过渡)
```
goUp() {
      let nowTop =
        document.body.scrollTop || document.documentElement.scrollTop; // 获取当前滚动条位置
      if (nowTop > 0) {
        window.requestAnimationFrame(this.goUp);
        window.scrollTo(0, nowTop - nowTop / 5);
      }
    }
    ```