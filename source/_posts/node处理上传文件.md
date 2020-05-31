title: node处理上传文件
author: 大白腿
tags:
  - node
categories:
  - node
date: 2020-05-24 16:27:00
---
 //上传图片
  ```js
  const multer = require("multer") //引入
  const upload = multer({
    dest: __dirname + '/../../upload'  //要存储的路径地址
  })
  app.post('/admin/api/upload',upload.single("file"),async (req,res)=>{
    const file = req.file
    res.send(file)  //返回结果
  })
```
需要静态文件托管，表示upload下面的文件是静态的
  ``app.use('/upload',express.static(__dirname+'/upload'))``