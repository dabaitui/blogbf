title: vue路由懒加载
author: 大白腿
tags:
  - vue
categories:
  - vue
date: 2020-05-24 14:55:00
---
```js
// import Home from '../views/Home.vue'
const Home = () => import('../views/Home.vue')
```