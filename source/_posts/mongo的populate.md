title: mongo的populate
author: 大白腿
tags:
  - mongoDB
categories:
  - mongoDB
date: 2020-05-24 16:22:00
---
 ``populate("parent")``关联集合使用parent关联谁了把谁找出来
复用后populate要改成这样
    
```js
  const queryOptions = {}
  if(req.Model.modelName==="Category"){
    queryOptions.populate = "parent"
  }
const items = await req.Model.find().setOptions(queryOptions  ).limit(10)
    ```