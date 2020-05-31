title: git本地仓库提交到远程仓库
author: 大白腿
tags:
  - git
categories:
  - git
date: 2020-05-28 20:09:00
---
## 连接
1.查看本地仓库与那些仓库链接呢
```
$ git remote -v
```
2.让本地仓库与远程仓库新建一个链接  //origin是随便起的链接名(可以改，不过一般都用这个)
```
$ git remote add origin https://github.com/XXXX   //github上的远程地址
```

![upload successful](/images/pasted-6.png)

3.取消链接
```
$ git remote rm origin
```

## 提交
1.提交前最好先拉取  //都是在交互历史区
```
$ git pull origin master  //master是分支
```
2.将本地代码提交到github（需要输入github的用户名和密码）
```
$ git push origin master
```

![upload successful](/images/pasted-7.png)

## 克隆
```
$ git clone github地址 别名//可以不设置默认是仓库名
```

![upload successful](/images/pasted-8.png)
