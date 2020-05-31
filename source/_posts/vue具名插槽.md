title: vue具名插槽
author: 大白腿
tags:
  - vue
categories:
  - vue
date: 2020-05-24 16:57:00
---

父
```html
    <CardList title="新闻资讯" :categorise="newsdata">//传入的数据
      <template #items="{categorise}">//从子组件获取到的处理过数据
        <div class="flex mt-3 font-md color-333" v-for="(item,index) in categorise.newsList" :key="index">
          <span>[{{item.Catname}}]</span>
          <span>丨</span>
          <span class="flex-1">{{item.title}}</span>
          <span>{{item.date}}</span>
        </div>
      </template>
    </CardList>
```
子
```html
    <swiper class="mt-2">
      <swiper-slide v-for="(v,i) in categorise" :key="i">
      //具名插槽 name是要跟外面#items对应的
        <slot name="items" :categorise="v"></slot>
      </swiper-slide>
    </swiper>
```