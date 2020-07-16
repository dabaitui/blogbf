title: 配置plugin插件完成html模板打包
author: 大白腿
tags:
  - webpack
categories:
  - webpack
date: 2020-06-14 10:05:00
---
## 引入plugin

![upload successful](/images/pasted-18.png)
```js
let HtmlWebpackPlugin = require("html-webpack-plugin")//导入plugin
```
需要下载依赖
``cnpm i html-webpack-plugin --save-dev``

## 写plugin

![upload successful](/images/pasted-19.png)
```js
    plugins:[
        new HtmlWebpackPlugin({
            //将index.html和index.js进行整合
            template:"./src/index.html" //要整合的html的路径
        })
    ]
 ```
 
 如果报错检查package.json里有没有webpack,没有就``npm i webpack --save-dev``
 
![upload successful](/images/pasted-20.png)