title: webpack热更新
author: 大白腿
tags:
  - webpack
categories:
  - webpack
date: 2020-06-14 10:58:00
---
## 全局安装 webpack-dev-server
``cnpm i webpack-dev-server -g``

## 配置热更新

```js
    // 热更新
    devServer:{
        //设置项目构建的路径
        contentBase:path.resolve(__dirname,"dist"),
        //启动gzip压缩，让浏览器可以更快的打开
        compress:true,
        //能够看见实时更新的端口号
        port:3000,
        //是否自动打开浏览器
        open:true   
    }
 ```
 
![upload successful](/images/pasted-23.png)

## 启动
``webpack-dev-server``