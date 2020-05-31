title: mongo刨根问底查法
author: 大白腿
tags:
  - node
  - mongoDB
categories:
  - mongoDB
date: 2020-05-24 16:46:00
---
//查找子级
见Caregory.js和index.js

见Caregory模型
```js
schema.virtual("children",{
    localField:"_id",
    foreignField:"parent",
    justOne:false,
    ref:"Category"
})

schema.virtual("newList",{
    localField:"_id",
    foreignField:"categories",
    justOne:false,
    ref:"Article"
})

```
index子路由
```js
    router.get("/news/list",async (req,res)=>{
        const parent = await Category.findOne({
            name:"新闻分类"
        }).populate({
            path:"children",
            populate:{
                path:"newList"
            }
        }).lean()
        res.send(parent)
    })
  ```