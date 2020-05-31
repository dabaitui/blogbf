title: axios拦截器
author: 大白腿
tags:
  - axios
  - vue
categories:
  - axios
date: 2020-05-24 16:52:00
---
```js
import axios from "axios"
import Vue from "vue"
import router from "./router"
const http = axios.create({
    baseURL: "http://localhost:3000/admin/api"
})

```


//加header
```js
http.interceptors.request.use(function (config) {
    if (localStorage.token) {
        //加Bearer是因为规范
        config.headers.Authorization = "Bearer " + (localStorage.token || '')
    }
    return config
}, function (err) {
    return Promise.reject(err)
})
```

//拦截全部请求错误
```js
http.interceptors.response.use(res => {
    return res
}, err => {
   调用了饿了么的message方法
    if (err.response.data.message) {
        Vue.prototype.$message({
            type: "error",
            message: err.response.data.message
        })
        if(err.response.status === 401){
            router.push("/login")
        }
    }
    return Promise.reject(err)
})

```
导出
```js
export default http
```