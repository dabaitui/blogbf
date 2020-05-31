title: 创建本地git仓库完成版本控制
author: 大白腿
tags:
  - git
categories:
  - git
date: 2020-05-26 20:10:00
---
创建本地git仓库
```
$ git init //会生成一个隐藏文件夹git
```
本地编写完代码后，将一些文件提交到暂存区
```
$ git add xxx  //将xxx提交到暂存区
$ git add . 或者 -A   //将所有最新修改的文件都提交到暂存区
```
把暂存区内容提交到历史区
```
$ git commit -m'这里写描述信息'
$ git log  //查看历史版本信息
$ git reflog //查看历史版本信息(包含回滚的信息)
```
将历史区的文件回滚到本地
```
$ git reset --hard xxxxxxxxxxxxxxxx   //xxx是要回退的版本号
```