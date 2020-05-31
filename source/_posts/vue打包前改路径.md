title: vue打包前改路径
author: 大白腿
tags:
  - axios
  - vue
categories:
  - vue
date: 2020-05-24 17:19:00
---
打包前
开发环境变量
```js
  const http = axios.create({
    // baseURL: "http://localhost:3000/admin/api"
    baseURL: process.env.VUE_APP_API_URL || "/admin/api"
    //      process.env.VUE_APP是固定的
})
```
建个.env.development文件
```js
VUE_APP_API_URL = http://localhost:3000/admin/api
```


vue.config.js里
```js
module.exports = {
    outputDir : __dirname +"/../server/admin",//编译到的目录
    //判断是否是生产环境是的话加/admin前缀
    publicPath:process.env.NODE_ENV === "production"
    ? "/admin/"
    : '/'
}
```