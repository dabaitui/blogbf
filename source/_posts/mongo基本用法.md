title: mongo基本用法
author: 大白腿
tags:
  - mongoDB
categories:
  - mongoDB
date: 2020-05-24 15:50:00
---
数据库(database)  集合(collection)  数据/文档(document)

查看数据库
语法：```show databases```

选择数据库
语法: ```use 数据库名```

删除数据库
1.```use 数据库名 ```  先选择目标数据库
2.```db.dropDatabase()```  删除数据库

查看集合
语法 ``` show collections```

创建集合```db.createCollection("集合名")```

删除集合```db.集合名.drop()```

*********增
语法: db.集合名.insert(JSON数据)
如：``` db.c1.insert({name:"xiaoming"})```
查看集合具体内容```db.c1.find()```

一次插入多条数据
```
db.c1.insert([
    {
        name:"aaa",
        age:5
    },
    {
        name:"bbb",
        age:6
    }
])
```
一次插入10条(mongoDB底层是js支持部分js语法)
```
for(var i = 0; i < 10;i++){
    db.c1.insert({name:"a"+1,age:i})
}
```


*********查
语法：```db.集合名.find({条件},{查询的列})```   []里的内容为可选内容
条件 如果不写或者{}代表查询所有数据
     查询age=6的   {age:6}  db.c1.find({age:6})
查询的列（可选）
     不写则查全部字段
     {age:1} 只显示age列
     {age:0} 除了age列
     db.c1.find({age:18},{age:1})  //查询age为18，只显示age的列
运算符时
 ```db.c1.find({键:{运算符:值}})```
```db.c1.find({age:{$in:[5,18]}}) ``` 获取年龄为5和18岁的数据
 运算符有
 $gt  大于
 $gte 大于等于
 $lt  小于
 $lte 小于等于
 $ne  不等于
 $in  in
 $nin not in
 
 ```db.c1.find({键:{运算符:值}}).pretty()```pretty()格式化数据用的，看着方便

 *********改
 语法: db.集合名.update(条件,新数据,是否新增,是否修改多条)
 是否新增(可选)：指条件匹配不到则插入数据true是插入这条数据，false是不插入  默认是不插入
 是否修改多条(可选)：将匹配到的数据都修改true是，默认false
 升级语法
 修改器  
 $inc    递增
 $rename 重命名列
 $set    修改列值
 $unset  删除列
 db.集合名.update(条件,{修改器:{键:值}})
 如 ```db.c1.update({name:"bbb"},{$set:{name:"ddd"}})```
 加2岁```db.c1.update({name:"ddd"},{$inc:{age:2}})```
 减```db.c1.update({name:"ddd"},{$inc:{age:-2}})```
综合使用```db.c1.update({name:"aaa"},{$set:{name:"abc"},$inc:{age:100},$rename:{who:"sex"},$unset:{other:true}})```

 *********删
 语法：```db.集合名.remove(条件,是否删除一条)```
 是否删除一条true是是，默认false不





排序
语法:```db.集合名.find().sort(JSON)```
如：``` db.ci.find().sort({age:-1})```
JSON 键是以这个排列 值是 1升序  -1降序



分页
Limit和skip
语法```：db.集合名.find().sort().skip(数字).limit(数字)```
如：``` db.ci.find().sort({age:-1}).skip(3).limit(3)```
.count  统计总数量
skip 跳过值得数量
limit 限制的数量




聚合查询
语法：```db.集合名.aggregate([
    {管道:{表达式}}
])```
如：``` db.c2.aggregate([
    {
        $group:{
            _id:"$sex",//以这个分组，null为不用分组
            rs:{$sum:"$age"} //具体内容
            }
        }
    ])```
    
    ```
 db.c2.aggregate(
     [
         {
             $group:{
                 _id:"$sex",
                 rs:{$sum:"$age"}
                 }
             }
         ]
     )
 db.c2.aggregate(
     [
         {
             $group:{
                 _id:"$sex",rs:{$sum:1}
                 }
            }
             ,
             {
                 $sort:{rs:-1}
             }
         ]
     )
 ```
！！！这里值是表的键名要加$
常用管道
$group  将集合中的文档分组，用于统计结果
$match  过滤数据，只要输出符合条件的文档
$sort   聚合数据进一步排序
$skip   跳过直到文档数
$limit  限制集合数据返回文档数

常用表达式
$sum  综合   $sum:1同count表示总数
$avg  平均
$max  最大值
$min  最小值





索引

创建索引语法:``` db.集合名.createIndex(待创建索引的列,(可选 额外选项))```
如 ``` db.c1.createIndex({name:1})```
待创建索引的列 {键:1,...,键:-1}
1代表升序-1代表降序 {age:1}表示创建age索引并按照升序的方式存储
额外选项 ：设置索引的名称或者唯一索引等等

删除索引语法：
全部删除：```db.集合名.dropIndexes()```
如 db.c1.dropIndex("name_1")
删除指定：```db.集合名.dropIndex(索引名)```

查看索引语法：```db.集合名.getIndexes()```

创建复合/组合索引:```db.集合名.creatIndex({键1:方式,键2:方式})```

创建唯一索引   //就是唯一不重复
``
db.集合名.createIndex(待添加的索引列,{unique:列名})
`` 列名可选
                                    
分析索引```db.集合名.find(条件).explain("executionStats")```
explain("executionStats")这个是看这次查询是用了什么方式查了多少次的具体信息

如：先创建索引 ```db.c1.createIndex({age:1})```
   再使用 ```db.c1.find({age:18}).explain("executionStats")```