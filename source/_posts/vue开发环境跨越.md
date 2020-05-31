title: vue开发环境跨越
author: 大白腿
tags:
  - js
  - vue
  - 跨域
categories:
  - vue
date: 2020-05-24 13:11:00
---
新建vue.config.js
```js
module.exports = {
    devServer: {
      proxy: {
        '/api': {
          target: 'http://localhost:3000',
          changeOrigin: true,
          pathRewrite:{
            '':''
          }
        }
      }
    }
  }
```