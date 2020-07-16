title: 创建本地git仓库完成版本控制
author: 大白腿
tags:
  - git
categories:
  - git
date: 2020-05-26 20:10:00
---
### 初始
创建本地git仓库，初始化
```
$ git init //会生成一个隐藏文件夹git
```
### 暂存区
可以在文件夹中新建几个文件之后
```
$ git status//查看文件状态
```
![upload successful](/images/pasted-59.png)
红框是未追踪的文件
git提示用add提交到暂存区
```
$ git add xxx  //将xxx提交到暂存区
$ git add . 或者 -A   //将所有最新修改的文件都提交到暂存区
$ git restore XXX //将XXX文件撤回修改
$ git diff //查看修改后不同的地方
$ git restore --staged XXX //将提交到暂存区的文件撤回（和add反着来）
```

![upload successful](/images/pasted-60.png)
现在将index.css提了上去
绿色就代表已追踪到的修改后的文件了，但是还没提交到历史区
这时先把index.css修改一下之后再看状态

![upload successful](/images/pasted-61.png)
它红色提示了modified,index.css已经被修改了
他上边提示了用add来提交这次修改，或者restore来撤回这次修改

提交之后再看下状态，就没问题了，之后就可以准备提交到历史区了
![upload successful](/images/pasted-62.png)

restore撤销修改
![upload successful](/images/pasted-69.png)
可以用diff查看修改后的区别
![upload successful](/images/pasted-71.png)
把这次提交到暂存区的文件取消
![upload successful](/images/pasted-75.png)
### 历史区

把暂存区内容提交到历史区
```
$ git commit -m'这里写描述信息'
$ git log  //查看历史版本信息
$ git reflog //查看历史版本信息(包含回滚的信息)
```
![upload successful](/images/pasted-63.png)
现在把文件都提上去了，再看看git的状态

![upload successful](/images/pasted-64.png)
就提示说目前没有任何修改了（工作区和暂存区一样没有区别）
刚才我又随便提交到了历史区一遍
现在用log看看版本信息
![upload successful](/images/pasted-65.png)
git reflog的样子
![upload successful](/images/pasted-66.png)
将历史区的文件回滚到本地
```
$ git reset --hard xxxxxxxxxxxxxxxx   //xxx是要回退的版本号前7位就行
$ git reset --hard HEAD^ //回退到上个版本,几个^就是回退几个版本^^^就是3个
```
![upload successful](/images/pasted-67.png)
这样就回退到上个版本了，本地的文件也直接替换了

![upload successful](/images/pasted-68.png)
回滚到某一版本号
### 删除文件
当我们需要删除暂存区或分支上的文件, 同时工作区也不需要这个文件了, 可以使用
```
git rm 文件名
git commit -m 'delete somefile'
git push
```
现在删除index.html
![upload successful](/images/pasted-76.png)
他提示说index.html已经被删了
之后用rm删除
![upload successful](/images/pasted-77.png)
如果只是想把index.html拿回来就只能版本回退了


当我们需要删除暂存区或分支上的文件, 但本地又需要使用, 只是不希望这个文件被版本控制, 可以使用
```
git rm --cached 文件名
git commit -m 'delete remote somefile'
git push
```