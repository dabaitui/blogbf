title: vue后台富文本
author: 大白腿
tags:
  - vue
categories:
  - vue
date: 2020-05-24 16:34:00
---
``npm install --save vue2-editor``
之后引入
``import { VueEditor } from 'vue2-editor'``

```js
components:{
    VueEditor
  },
 ```

  ```html
  <el-form-item label="详情">
        <vue-editor v-model="model.body"></vue-editor>
      </el-form-item>
      ```
自己上传图片
```html
<vue-editor useCustomImageHandler @image-added="handleImageAdded" v-model="model.body"></vue-editor>
```
```js
  methods: {
    async handleImageAdded(file, Editor, cursorLocation, resetUploader) {
      const formData = new FormData();
      formData.append("file", file);
              //字段名,可以随便改，el好像是file
      const res =await this.$http.post("/upload",formData)
      Editor.insertEmbed(cursorLocation, "image", res.data.url);
      resetUploader();
    },
  }
 ```