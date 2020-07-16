title: webpack初体验
author: 大白腿
tags:
  - webpack
categories:
  - webpack
date: 2020-06-12 20:34:00
---
## 全局安装
```
cnpm install webpack webpack-cli -g //安装webpack和cli
```

## 新建文件夹
```
npm init -y  //可以初始化一个package.json
```
## 之后在此文件夹安装webpack
```
cnpm install webpack webpack-cli --save-dev  //保存到开发模式
```

## 安装好后就能在配置里看见了

![upload successful](/images/pasted-15.png)

## 打包
1.先随便写点东西
2.开发模式下的打包(有注释和换行)
```
webpack ./src/index.js -o ./dist/bundle.js --mode=development
```
``./src/index.js是入口文件``
``-o ./dist/bundle.js是指定输出的文件路径``
``--mode=development表示开发模式``
3.生产模式下打包(压缩代码)
```
webpack ./src/index.js -o ./dist/bundle_s.js --mode=production
```