title: mongo将所有模型引入插件
author: 大白腿
tags:
  - node
  - mongoDB
categories:
  - mongoDB
date: 2020-05-24 16:43:00
---
将所有模型东西引用进来
``npm i require-all``
在db里
``require("require-all")(__dirname + '/../models')``