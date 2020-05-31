title: node生产token插件
author: 大白腿
tags:
  - node
categories:
  - node
date: 2020-05-24 16:41:00
---
token插件
``npm i jsonwebtoken``
全局index.js里
       名        值
``app.set("secret","666666666")``

子路由里 
 ```
    const jwt= require("jsonwebtoken")
    const token = jwt.sign({id:user._id},app.get("secret"))
    res.send({token})
```