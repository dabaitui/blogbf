title: webpack配置文件打包
author: 大白腿
tags:
  - webpack
categories:
  - webpack
date: 2020-06-14 09:03:00
---
## 新建webpack.config.js

## 写配置信息
```js
let path = require("path")//导入path
module.exports = {
    //入口文件
    entry:'./src/index.js',
    //出口文件
    output:{
        //输出的文件名
        filename:"bundle.js",
        //输出的路径  绝对路径  这句意思就是当前目录下的dist文件夹
        path:path.resolve(__dirname,"dist")//获取当前目录
    },
    //模式  开发development/生产production
    mode:"development"
}
```

## 打包 - 直接webpack即可
```
webpack
```

