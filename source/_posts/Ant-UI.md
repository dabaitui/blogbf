title: Ant UI
author: 大白腿
tags:
  - ant
  - react
categories:
  - react
date: 2020-06-27 15:26:00
---
### 安装
```
npm install antd-mobile --save
```

### 样式全部导入，组件单独导入
```
import 'antd-mobile/dist/antd-mobile.css'

import {Button} from "antd-mobile"

ReactDOM.render(
  <Button>Start</Button>,
  document.getElementById('root')
);


```

### 按需加载
1.安装babel-plugin-import
```
cnpm i babel-plugin-import --save
```
2.配置babel-plugin-import
```
npm run eject //让隐藏的配置文件显示出来
```
如果报错

![upload successful](/images/pasted-34.png)
3.package.json里最后加上
```
    "plugins": [
        ["import", { "libraryName": "antd-mobile", "style": "css" }]
    ]
    ```
    

![upload successful](/images/pasted-36.png)
4.之后使用时只需要引组件就行，css会自动按需加载

![upload successful](/images/pasted-37.png)