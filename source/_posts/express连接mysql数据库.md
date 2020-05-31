title: express连接mysql数据库
author: 大白腿
tags:
  - node
  - express
  - mysql
categories:
  - node
date: 2020-05-24 13:14:00
---
1.安装
```
npm install mysql
```
2.新建db文件夹=>新建sql.js文件
https://github.com/mysqljs/mysql //给的官方例子

sql.js里
```js
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'root',
  password : 'root',
  database : 'demo1'
});
module.exports=connection

server=>router=>index.js
var connection = require("../../db/sql.js")
router.get('/api/list', function(req, res, next) {
  connection.query('SELECT * from dome', function (error, results, fields) {
    res.json(results)
  })
});
```
