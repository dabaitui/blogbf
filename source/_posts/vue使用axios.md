title: vue使用axios
author: 大白腿
tags:
  - vue
  - axios
categories:
  - axios
date: 2020-05-24 15:25:00
---

安装
```
 npm install --save axios
```
main.js
```js
import axios from 'axios'
Vue.prototype.axios = axios;
```
//在这个里面反向代理
vue.config.js里  
```js
module.exports = {
    devServer: {
      proxy: {
        '/api': {
          target: 'http://39.97.33.178',
          changeOrigin: true
        }
      }
    }
  }
```
使用
```js
    this.axios.get("/api/movieOnInfoList?cityId=10").then(res => {
      console.log(res);
    });
```

post
```js
      this.axios
        .post(
          "/api/message.php",
          {
            name:name,
            tel: tel,
            text: text,
          },
          {
            headers: {
              "Content-Type": "application/json;charset=UTF-8"
            }
          }
        )
        .then(res => {
          console.log(res)
        });
  ```