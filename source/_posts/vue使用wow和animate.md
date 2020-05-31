title: vue使用wow和animate
author: 大白腿
tags:
  - vue
categories:
  - vue
date: 2020-05-24 15:15:00
---
// wow
（1）通过npm安装：

```
npm install wowjs --save-dev
```

animate.css会自动安装。

（2）在main.js中引入animate.css

import 'animate.css'
在组件需要的地方引入wowjs

有两种使用方式：
```

1.?import {WOW} from 'wowjs'? ? mounted() { new WOW().init() }

2.import WOW from 'wowjs'? ? mounted() { new WOW.WOW().init() }
```

下面给出在实例中的应用：

```html
<template>
  <div class="caselist">
    <ul class="clearfix">
      <li class="wow slideInUp" v-for="(item, index) in cases" :key="index">
      </li>
    </ul>
  </div>
</template>
```
 
```js
<script type="text/ecmascript-6">
  import {WOW} from 'wowjs'
 
  export default {

    //不常用
    //props: ['cases'],
    //watch: {
    //  cases() {
    //    this.$nextTick(() => { // 在dom渲染完后,再执行动画
    //      var wow = new WOW({
    //        live: false
    //      })
    //      wow.init()
    //    })
    //  }
    //}

    //常用方法
      mounted() {
        // 在项目加载完成之后初始化wow
        this.$nextTick(() => {
          let wow = new WOW({
            live: false
          });
          wow.init();
        });
      }
  }
</script>
```
