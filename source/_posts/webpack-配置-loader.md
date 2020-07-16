title: webpack 配置 loader
author: 大白腿
tags:
  - webpack
categories:
  - webpack
date: 2020-06-14 09:41:00
---
## 举例 先在index.js 里引入个css文件

![upload successful](/images/pasted-16.png)

## 配置webpack
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
    mode:"development",
    // loader配置
    module:{
        //对某个格式的文件进行转换处理
        rules:[
            {
                test:/\.css$/, //配置后缀名为css的文件（需要正则）
                //告知怎么处理，use数组中的loader有顺序要求，是从下到上的顺序
                use:[
                    //将js的样式内容插入到style标签里面
                    "style-loader",
                    // 将css文件转换为js
                    "css-loader"
                ]
            }
        ]
    }
}
```

!! 这时直接编译会报错

![upload successful](/images/pasted-17.png)
提示没有所需要的依赖

## 安装依赖
``cnpm install style-loader css-loader --save-dev``

之后打包就没问题了