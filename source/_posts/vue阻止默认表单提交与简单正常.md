title: vue阻止默认表单提交与简单正则
author: 大白腿
tags:
  - vue
categories:
  - vue
date: 2020-05-24 15:01:00
---
```
 <form v-on:submit.prevent="tj"> 阻止提交页面刷新 并执行 tj()方法 form里写
 ```
 @submit.native.prevent="save"
 提交    原生    阻止
//获取dom元素
```html
<input placeholder="您的电话" type="number" name id ref="tel" />
<input class="tj" value="提交留言" type="submit" />
```
```js
    tj() {
      var tel = this.$refs.tel.value;
      var name = this.$refs.name.value;
      var text = this.$refs.text.value;
      if (name == "") {
        alert("姓名不能为空");
        return false;
      } else if (tel == "") {
        alert("手机号不能为空");
        return false;
      } else if (text == "") {
        alert("留言内容不能为空");
        return false;
      } else if (!/^1[3456789]\d{9}$/.test(tel)) {
        alert("手机号格式不正确");
        return false;
      }
      console.log(name,tel,text);
    }
   ```