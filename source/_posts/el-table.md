title: el-table
author: 大白腿
tags:
  - element
categories:
  - element
date: 2020-05-24 15:41:00
---
```html
    <el-table :data="items"> //要遍历的数组
      <el-table-column prop="_id" label="ID" width="230"></el-table-column> //prop是值
      <el-table-column prop="title" label="标题"></el-table-column>
      <el-table-column fixed="right" label="操作" width="180">
        //slot-scope="scope" 当前目标的内容存到scope里
        <template slot-scope="scope">
          <el-button
            type="text"
            size="small"
            @click="$router.push(`/articles/edit/${scope.row._id}`)"
          >编辑</el-button>
          <el-button type="text" size="small" @click="remove(scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
```