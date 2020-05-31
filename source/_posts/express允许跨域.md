title: express允许跨域
author: 大白腿
tags:
  - express
  - node
  - js
  - 跨域
categories:
  - node
date: 2020-05-24 13:12:00
---
app.js里
```js
router.all('*', function(req, res, next) {
   res.header("Access-Control-Allow-Origin", "*");
   res.header("Access-Control-Allow-Headers", "X-Requested-With");
   res.header("Access-Control-Allow-Methods","PUT,POST,GET,DELETE,OPTIONS");
   res.header("X-Powered-By",' 3.2.1');
   res.header("Content-Type", "application/json;charset=utf-8");
   next();
});
```