title: mongo权限
author: 大白腿
tags:
  - mongoDB
categories:
  - mongoDB
date: 2020-05-24 15:44:00
---
***!权限机制!***
步骤1
```
mongo
use admin
```

创建账号
```js
db.createUser({
    "user":"账号",
    "pwd":"密码",
    "roles":[
        {
            role:"角色",
            db:"所属数据库"
        }
    ]
})
db.createUser({
    "user":"admin",
    "pwd":"yhq990807",
    "roles":[
        {
            role:"root",
            db:"admin"
        }
    ]
})
db.createUser({
    "user":"wz",
    "pwd":"yhq990807",
    "roles":[
        {
            role:"readWrite",
            db:"wz"
        }
    ]
})
```
步骤2
退出卸载服务
```
mongod --remove  //一定要管理员运行
```

步骤3
创建要身份验证的mongoDB服务
```
mongod --install --dbpath G:\mongodb-win32-x86_64\mongodb-win32-x86_64-2012plus-4.2.3\data --logpath G:\mongodb-win32-x86_64\mongodb-win32-x86_64-2012plus-4.2.3\logs\mongodb2.log --auth
```
 --auth表示需要身份验证

步骤4
进入服务
mongo后不会警报了
通过超级管理员身份账号登录
方法1：mongo 服务器IP地址:端口/数据库 -u 用户名 -p 密码
    如：```mongo 127.0.0.1:27017/admin -u admin -p yhq990807```
方法2：
```
a-先登录  b-选择数据库  c-输入db.auth(用户名,密码)
  mongo     use admin    db.auth("admin","yhq990807")
        ```