title: mongo备份与还原
author: 大白腿
tags:
  - mongoDB
categories:
  - mongoDB
date: 2020-05-24 15:47:00
---
备份数据
导出数据语法：```mongodump -h -prot -u -p -d -o```
-h host 服务器ip地址（一般不写默认本机）
-prot   端口（一般不写默认27017）
-u user 账号
-p pwd  密码
-d database 数据库（不写则导出全部）
-o open  备份到指定目录下
备份全部数据库     要在bin目录下执行
```
mongodump -u admin -p yhq990807 -o G:\mongodb-win32-x86_64\mongodb-win32-x86_64-2012plus-4.2.3\bak
```
备份指定数据库     要在bin目录下执行
```
mongodump -u admin -p yhq990807 -d admin -o G:\mongodb-win32-x86_64\mongodb-win32-x86_64-2012plus-4.2.3\bak2
```
user是要备份的数据库的用户

还原/导入数据
备份数据目录```mongorestore -h -prot -u -p -d --drop``` 
-d  不写则还原全部数据
--drop 先删除数据库再导入，不写则直接覆盖
还原全部数据
```
mongorestore -u admin -p yhq990807 --drop G:\mongodb-win32-x86_64\mongodb-win32-x86_64-2012plus-4.2.3\bak
```
还原指定数据库
```
mongorestore -u admin -p yhq990807 -d test4 --drop G:\mongodb-win32-x86_64\mongodb-win32-x86_64-2012plus-4.2.3\bak2\test4
```
也是要有权限的用户操作
