title: node散列密码
author: 大白腿
tags:
  - node
  - mongoDB
categories:
  - mongoDB
date: 2020-05-24 16:36:00
---
``npm i bcrypt``下载插件

模型里
```
const schema = new mongoose.Schema({
    name:{type:String},
    pwd:{
        type:String,
        select:false,//不会被查出来
        //怎么保存这个数据
        set(val){
                       			异步    值   加密程度10-12
            return require("bcrypt").hashSync(val,10)
        }
    },
})
```
  ``const user =await adminUser.findOne({name}).select("+password")``查询时强制获取password
  
 校验密码
    ```
    const isValid = require("bcrypt").compareSync(pwd, user.pwd)
    if (!isValid) {
      return res.status(422).send({
        message: "密码错误"
      })
    }
    ```