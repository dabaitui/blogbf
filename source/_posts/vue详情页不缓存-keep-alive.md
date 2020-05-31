title: vue详情页不缓存(keep-alive)
author: 大白腿
tags:
  - vue
categories:
  - vue
date: 2020-05-24 15:13:00
---
```html
    <keep-alive>
        <router-view v-if="$route.meta.keepAlive"></router-view>
    </keep-alive>
    <router-view v-if="!$route.meta.keepAlive"></router-view>
```