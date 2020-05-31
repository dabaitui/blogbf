title: node常用
author: 大白腿
tags:
  - node
categories:
  - node
date: 2020-05-24 16:10:00
---
运行``node ----- node index.js``
```
setImmediate 下一帧
console.log(__filename)//当前文件位置
console.log(__dirname)//当前文件所在目录
console.log(process)//全局变量
console.log(process.argv)//能获取执行时后面带的参数 如：node index.js xxxxx
process.stdin.on("data",e=>{ //持续运行
    console.log(1)
})
```
npm init 创建npm环境