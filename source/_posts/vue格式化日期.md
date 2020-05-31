title: vue格式化日期
author: 大白腿
tags:
  - vue
categories:
  - vue
date: 2020-05-24 17:17:00
---
 ``npm i dayjs``

引入 ``import dayjs from "dayjs"``
```html
  <span>{{item.createdAt | Data}}</span>
```
```js
filters:{
    Date(val){
      //两位数的月份，两位数的日期
      return dayjs(val).format('MM/DD')
    }
  },
 ```