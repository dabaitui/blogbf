title: vue父子通信
author: 大白腿
tags:
  - vue
categories:
  - vue
date: 2020-05-24 15:05:00
---
//路由传参 父==>子
父
```js
      this.$router.push({
        path: a + "/bookShow/" + bookId,
        query: { bookId: bookId }
      });
      或
      在router中
      {
        path: '/heros/edit/:id',
        name: 'HeroEdit',
        component: HeroEdit,
        props:true //这句
      },
 ```
子
```js
    this.bookId = this.$route.query.bookId;
    或
    props:[] //直接能拿到
 ```
 
 //子 ==》 父传参
子
```
 <div @click="active"></div>
 data:activeMenu...
  methods: {
    active() {
      this.activeMenu = !this.activeMenu;
      this.$emit("active", this.activeMenu);
    }
  }
  ```
父
```
<Header @active="active" />
 data:activeMenu...
  methods: {
    active(data) {
      this.activeMenu = data;
      console.log(this.activeMenu);
    }
  }
  ```
