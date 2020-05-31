title: node转换大小写插件
author: 大白腿
tags:
  - node
categories:
  - node
date: 2020-05-24 16:26:00
---
 ``cnpm i inflection``转换类名的东西比如：大小写，单复数
``const modelName = require("inflection").classify(req.params.resource)``
``const Category = require(`../../models/${modelName}`)``
 这个操作是把小写复数的改成大写单数的