title: express-generator的使用
author: 大白腿
tags:
  - js
  - node
  - express
categories:
  - node
date: 2020-05-24 13:07:00
---
1.全局安装
```
npm install express-generator -g
```
2.创建项目
``` 
   express --view=ejs 名字
```
例: express --view=ejs server
之后按提示走
默认端口3000

3.routes=>index.js里

注意：本地最好不用localhost要用ip
查看ip
cmd  之后输入  ipconfig
```js
router.get('/api/list', function(req, res, next) {
  res.json({
    a:1,
    b:2
  })
});
```