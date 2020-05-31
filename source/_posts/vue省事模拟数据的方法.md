title: vue省事模拟数据的方法
author: 大白腿
tags:
  - vue
categories:
  - vue
date: 2020-05-24 16:56:00
---
      newsdata:[
        {
          name:"热门",
          newsList:new Array(5).fill({}).map(()=>({
              Catname:"公告",
              title:"未成年人防沉迷新规接入公告",
              date:"09/21"
          }))
        }
      ],