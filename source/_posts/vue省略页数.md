title: vue省略页数
author: 大白腿
tags:
  - vue
categories:
  - vue
date: 2020-05-24 15:22:00
---
```
  v-if="pageActive-2<=index&&index<=(pageActive+2<5?5:pageActive+2)"
 ```
5页例子
 ```html
  <span v-if="pageActive>2" class="sl">...</span>
   <span
        @click="toPage(index)"
        :class="{active:index===pageActive}"
        v-for="(item,index) in ye"
        :key="index"
        v-if="pageActive-2<=index&&index<=(pageActive+2<5?5:pageActive+2)"
        class="ye"
      >{{item}}</span>
   <span v-if="pageActive<ye-3" class="sl">...</span>
  ```