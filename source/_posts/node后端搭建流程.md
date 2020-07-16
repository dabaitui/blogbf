title: node后端搭建流程
author: 大白腿
tags:
  - node
  - express
  - element
categories:
  - node
date: 2020-07-09 17:57:00
---
### 初始化

先建个如server的文件夹，之后``npm init -y``先初始化一下项目
新建个index.js

之后去package.json里配置一下热更新``    "serve": "nodemon index.js",``
这样就可以像启动vue一样``npm run serve``来启动服务器了

![upload successful](/images/pasted-40.png)
如果没有nodemon需要先全局安装一下


### 写服务端接口的准备工作

先把常用的插件先下来下如：npm i express@next mongoose cors 等

之后在index.js里
```js
const express = require("express")

const app = express()


app.listen(3000,()=>{
    console.log("http://localhost:3000")
})
```

之后新建个如routes的文件夹开始写路由

![upload successful](/images/pasted-41.png)

routes/admin/index
```js
module.exports = app =>{
    const express = require("express")
    const router = express.Router()//用到了子路由
    router.post("/categories",async (req,res)=>{
        
    })
    app.use("/admin/api",router)
}
```
这里接收个参数app需要在index.js里传过来
``require("./routes/admin/index")(app)``

![upload successful](/images/pasted-42.png)

### 开始连接mongo数据库

建议新建个如plugins的文件夹,之后建个db.js的文件，用来连接数据库
```js
module.exports = app =>{
    const mongoose = require("mongoose")//引用mongoose
    //连接数据库 127.0.0.1:27017 是默认地址   bsdz是数据库名
    mongoose.connect('mongodb://127.0.0.1:27017/bsdz',{
        useNewUrlParser : true,
        useUnifiedTopology: true
    })
}
```

这时服务端的文件结构是这样的

![upload successful](/images/pasted-43.png)

之后在index.js里引用一下db.js，把app传进去（和routes一样）
``
require("./plugins/db")(app)
``

### 创建模型

新建个models的文件夹用来存放模型
新建个模型文件如：Category.js
```js
const mongoose = require("mongoose")//引入mongo

//每一个schema就是一个文件，整个模型是一个集合
const schema = new mongoose.Schema({
    //开始定义需要的字段 name是key ,type是类型
    name:{
        type:String
    }
})

module.exports = mongoose.model("Category",schema)
```
去index.js里去使用
```js
module.exports = app => {
    const express = require("express")
    const router = express.Router()//用到了子路由
    const Category = require("../../models/Category")//引入模型
    router.post("/categories", async (req, res) => {
        await Category.create(req.body)//将传进来的内容创建到集合中
        res.send(model)//发送到客户端
    })
    app.use("/admin/api", router)
}
```
这时需要去index.js里写个处理数据的中间件,顺便把cors跨域模块也引进来
```
app.use(require("cors")())//跨域模块
app.use(express.json())//处理req.body
```

![upload successful](/images/pasted-44.png)

前端写个axios试试好不好使
```js
    async save() {
      const res = await this.axios.post("categories", this.model);
      if (res.data) {
        this.$router.push("/categories/list");
        this.$message({
          type: "success",
          message: "保存成功"
        });
      }
    }
```
如果这里报错了，有可能是mongodb设置权限了，需要给用户添加权限

这样新建分类的接口就写好了，
之后同理写个分类列表的接口
```js
    router.get("/categories", async (req, res) => {
        const items = await Category.find().limit(10)//查找所有数据，限制10条
        res.send(items)//发送到客户端
    })
```


### 在后台编辑分类

先定义一个点击事件，点击时跳转到分类的详情页
```html
        <el-button type="primary" size="small"
         @click="$router.push(`/categories/edit/${scope.row._id}`)">编辑</el-button>
```
![upload successful](/images/pasted-45.png)

之后去路由里解耦

![upload successful](/images/pasted-46.png)
这样详情页就可以直接props:[id]拿到传过来的id了

拿到id后就可以请求详情页的数据了
```js
  methods:{
      async fetch(){
          const res = await this.axios.get(`/categories/${this.id}`)
          this.model = res.data
      }
  },
  created(){
      //有id才会执行fetch
      this.id && this.fetch()
  }
 ```
 但是这时候后端详情的接口还没有，就需要去后端写详情接口了
 
 ```js
     //详情接口
    router.get("/categories/:id", async (req, res) => {
        const model = await Category.findById(req.params.id)//通关id找
        res.send(model)//发送到客户端
    })
 ```
 
 
 后台保存时需要判断是新建还是编辑，走不同的接口
 ```js
     async save() {
      let res;
      if (this.id) {
      	//如果有id就是编辑走put
        res = await this.axios.put(`categories/${this.id}`, this.model);
      } else {
      //没有就算新建走post
        res = await this.axios.post("categories", this.model);
      }
      if (res.data) {
        this.$router.push("/categories/list");
        this.$message({
          type: "success",
          message: "保存成功"
        });
      }
    }
 ```
 
 之后去后端定义编辑的put接口
 ```js
    //编辑接口
    router.put("/categories/:id", async (req, res) => {
        const model = await Category.findByIdAndUpdate(req.params.id,req.body)//通过id找之后更新,两个参数第一个是要找的id，第二个就是要更新的数据
        res.send(model)//发送到客户端
    })
 ```
 
 
 ### 删除分类
 
 先定义一个删除事件
 ```html
        <el-button type="primary" size="small"
         @click="remove(scope.row)">删除</el-button>
```
参数是这整个一行的数据scope.row

定义删除方法
```js
    async remove(row) {
    //element的提示框组件
      this.$confirm(
        `此操作将永久删除${row.name}这个分类的数据, 是否继续?`,
        "注意",
        {
          confirmButtonText: "确定",
          cancelButtonText: "取消",
          type: "warning"
        }
      ).then(async () => {
        const res = await this.axios.delete(`categories/${row._id}`);
        this.fetch();
        this.$message({
          type: "success",
          message: "删除成功!"
        });
      });
    }
```
去后端写删除的接口
```js
    //删除接口
    router.delete("/categories/:id", async (req, res) => {
        const model = await Category.findByIdAndDelete(req.params.id)//通过id找之后更新,参数是要删除的id
        res.send({
            success: true
        })//发送到客户端
    })
 ```
 ### 上级分类
 
 现在，需要加一个上级分类，用来保存所有分类的对应关系
 ```html
       <el-form-item label="上级分类">
        <el-select v-model="model.parent">
          <el-option v-for="item in parents" :key="item._id" :label="item.name" :value="item._id"></el-option>
        </el-select>
      </el-form-item>
   ```
   
   后端需要在模型里添加字段
 ```js
 const schema = new mongoose.Schema({
    //上级分类
    parent:{
        type:mongoose.SchemaTypes.ObjectId,//因为保存的是其他集合的id，所以要这么写
        ref:'Category'//这里是关联哪个模型

    },
    //开始定义需要的字段 name是key ,type是类型
    name:{
        type:String
    }
})
 ```
 
 这时在列表页就可以拿到上级分类的id了
 
![upload successful](/images/pasted-47.png)
但是，上级分类这里显示的是id，正常来说应该显示的是分类名字，这样更直观，所以需要改列表页的接口
```js
    //列表接口
    router.get("/categories", async (req, res) => {
        const items = await Category.find().populate("parent").limit(10)//查找所有数据，限制10条   如果数据库中有关联字段，就可以用populate查出来,传进去什么字段，就会直接找对应字段id所属的集合的所有信息，而不仅仅是id了
        res.send(items)//发送到客户端
    })
 ```
![upload successful](/images/pasted-48.png)


### 通用CRUD接口


将app.use里的路由定义成动态路由
``    app.use("/admin/api/rest/:resource", router)``

![upload successful](/images/pasted-49.png)
之后可以将路由中的categories都删了
因为需要按照路由引入对应的模型所有这个就不能要了
`` const Category = require("../../models/Category")//引入模型``
```js
    const router = express.Router({
        mergeParams:true//上面添加这句，表示合并参数，因为内部要用
    })//用到了子路由
 ```
 之后console一下就可以拿到动态路由的名了
 
![upload successful](/images/pasted-50.png)

![upload successful](/images/pasted-51.png)

但是现在名字是小写复数，模型名是大写单数
就需要用inflection包来进行单复数转换
``npm i inflection --save``
列表页接口为例
```js
  router.get("/", async (req, res) => {
        const ModelName = require("inflection").classify(req.params.resource)//转类名大小写，单复数
        const Model = require(`../../models/${ModelName}`)
        const items = await Model.find().populate("parent").limit(10)//查找所有数据，限制10条   如果数据库中有关联字段，就可以用populate查出来,传进去什么字段，就会直接找对应字段id所属的集合的所有信息，而不仅仅是id了
        res.send(items)//发送到客户端
    })
```

由于重复的地方太多，可以把引入模型和大小写转换放到一个中间件里执行

```js
    app.use("/admin/api/rest/:resource",
        async (req, res, next) => {
            const ModelName = require("inflection").classify(req.params.resource)//转类名大小写，单复数
            // const Model = require(`../../models/${ModelName}`)
            //由于这样后面的中间件是拿不到这个Model的，所以要把他添加到req中
            req.Model = require(`../../models/${ModelName}`)
            next()
        }, router)
 ```
 就可以将路由中的categories全删了，Category模型全换成req.model
 
 
![upload successful](/images/pasted-52.png)
这时注意这里

![upload successful](/images/pasted-53.png)
这个查找分类的上级，但是现在是通用的接口，现在这么做就不合适了，需要改成条件选择
```js
//列表接口
    router.get("/", async (req, res) => {
        const queryOptions = {}
        if(req.Model.modelName === "Category"){
            queryOptions.populate = "parent"
        }
        //如果数据库中有关联字段，就可以用populate查出来,传进去什么字段，就会直接找对应字段id所属的集合的所有信息，而不仅仅是id了
        const items = await req.Model.find().setOptions(queryOptions).limit(10)//查找所有数据，限制10条   
        res.send(items)//发送到客户端
    })
```


### 图片上传

前端用element的upload定义个上传图像组件
```html
      <el-form-item label="缩略图">
        <!--
               action里是上传的地址
               :on-success 是成功后做什么
               :before-upload 是上传前做什么
        -->
        <el-upload
          class="avatar-uploader"
          :action="axios.defaults.baseURL + '/upload'"
          :show-file-list="false"
          :on-success="afterUpload"
        >
          <!-- 判断有没有图片，有就展示图片没有就展示icon -->
          <img v-if="model.smallImg" :src="model.smallImg" class="avatar" />
          <i v-else class="el-icon-plus avatar-uploader-icon"></i>
        </el-upload>
      </el-form-item>
```
```js
	//先打印看看
    afterUpload(res) {
        console.log(res)
    },
```
这时会报后端找不到的错误
这时去后端定义接口地址
这里需要一个处理图片的中间件，可以用multer
``npm i multer``
```js
    // 图片上传
    const multer = require("multer")//引入multer
    //上传的中间件 dest 是目标地址
    const upload = multer(
        {dest:__dirname+"/../../uploads"}
    )
    //upload.single("file") 单个文件上传用single,参数是form data里的名字file
    app.post("/admin/api/upload",upload.single("file") ,async (req, res) => {
        const file = req.file
        file.url = `http://localhost:3000/uploads/${file.filename}`//添加http的地址
        res.send(file)
    })
```
现在uploads里就已经有图片了，
这时需要去根index里加个静态文件的托管
```js
app.use("/uploads",express.static(__dirname+"/uploads"))
```
去前端补全afterUpload方法
```js
    afterUpload(res) {
        this.$set(this.model,'smallImg',res.url)
    },
 ```
 element在列表中展示图片
 ```html
      <el-table-column label="产品名称">
          <template slot-scope="scope">
              <img :src="scope.row.smallImg" style="height:3rem" alt="">
          </template>
      </el-table-column>
```



### 富文本
可以用  Vue2Editor
https://www.npmjs.com/package/vue2-editor

先下载
``npm install vue2-editor``

在script中引进来
``import { VueEditor } from "vue2-editor";``

![upload successful](/images/pasted-54.png)

注册组件
```js
  components: {
    VueEditor
  },
 ```
![upload successful](/images/pasted-55.png)

去html中使用
```html
      <el-form-item label="介绍">
        <vue-editor v-model="model.text"></vue-editor>
      </el-form-item>
```

后端模型中定义个String接收就行了
```js
    // 介绍
    text:{
        type:String
    }
 ```
 
 这样就已经可以用了
 但是现在有个问题，就是图片存储方式
 
![upload successful](/images/pasted-56.png)
默认行为是直接把图片进行base64编码了，好处就是方便，坏处就是会造成这个接口体积过大，所以要改成之前上传图片的方式
```html
      <el-form-item label="介绍">
        <!-- useCustomImageHandler使用自定义图片处理事件  image-added是图片上传后做什么事 -->
        <vue-editor useCustomImageHandler @image-added="handleImageAdded" v-model="model.text"></vue-editor>
      </el-form-item>
```
```js
    //富文本图片上传
    async handleImageAdded(file, Editor, cursorLocation, resetUploader) {
      const formData = new FormData(); //html自带的方法，用于提交表单数据
      formData.append("file", file); //字段名是file
      const res = await this.axios.post("upload", formData);
      Editor.insertEmbed(cursorLocation, "image", res.data.url);//三个参数，第一个是光标位置，第二个是告诉插入一张图片，第三个是图片地址
      resetUploader();
    },
 ```
 现在图片就是个网络地址了
 
 
 
 ### 登录权限问题
 
 密码不应该明文保存，应该存储的是加密过的数据
 所以要把密码加工一下
 改密码的模型加个set处理方法

 set里要进行散列密码，需要用个模块bcrypt来散列密码
 ``npm i bcrypt``
  ```js
    password:{
        type:String,
        select:false,//查询时这个字段不会被查出来,防止二次报错时对散列过的密码进行二次散列
        set(value){
            return require("bcrypt").hashSync(value,10)//散列的方法,两个参数第一个是要散列的密码，第二个是加密指数，越大越安全，但是越耗时一般10-12就可以了
        }
    }
 ```
 现在保存后密码就被散列了
 
![upload successful](/images/pasted-57.png)

之后写个登录页，能提交用户名密码就行

之后去后端定义一个验证登录的接口
```js
    //登录验证
    app.post("/admin/api/login",async (req,res)=>{
        const {name,password} = req.body
        // 根据用户名找用户 
        const Admin = require("../../models/Admin")
        const user = await Admin.findOne({name})
        if(!user){
            // 如果没有
            return res.status(422).send({
                message:"用户不存在"
            })
        }
        // 校验密码
        // 返回token
    })
 ```
 这里先写一半，这里用户如果不存在就会返回一个错误码,前端需要根据这个错误码在页面上做出提示
 
去axios里加个拦截器
```js
import axios from "axios"
import Vue from "vue"
const http = axios.create({
    baseURL: "http://localhost:3000/admin/api"
})
//后拦截器
http.interceptors.response.use(res => {
    return res //没问题就直接return
}, err => {
    if (err.response.data.message) {
        //console.log(err.response.data.message)报错的响应数据
        Vue.prototype.$message.error(err.response.data.message)//现在vue实例上有element，可以直接用$message这个弹出框
    }
    return Promise.reject(err)//有问题就返回报错
})
export default http
```
现在前端捕获完错误了，可以回过头写后端验证登录的接口了

```js
    //登录验证
    app.post("/admin/api/login",async (req,res)=>{
        const {name,password} = req.body
        // 根据用户名找用户 
        const Admin = require("../../models/Admin")
        const user = await Admin.findOne({name}).select("+password")
        //因为之前模型中密码的select设成false里，默认是查不到的，所有加上select("+password")来强制获取密码，- 就是排除
        if(!user){
            // 如果没有
            return res.status(422).send({
                message:"用户不存在"
            })
        }
        // 校验密码
        const isValid = require("bcrypt").compareSync(password,user.password)//用bcrypt的compareSync来验证密码，第一个参数是明文（提交上来的）,第二个是密文(数据库里存的)
            if(!isValid){
            //密码不对
            return res.status(422).send({
                message:"密码错误"
            })
        }
        // 返回token
    })
 ```
 现在差返回个token，可以用jsonwebtoken插件来解决
   ``npm i jsonwebtoken``
   ```js
           // 返回token
        const jwt = require("jsonwebtoken")
        const token = jwt.sign({id: user._id},"sybsdz")//用来生成token,第一个参数是个对象，里面的东西是想散列的东西,第二个参数是个秘钥(自己定义，随便写   )，之后会根据自己内部的算法来生成个token
        res.send({token})
   ```
   现在前端就可以拿到token了,接着补全登录方法
   
![upload successful](/images/pasted-58.png)
```js
    async login() {
      if (!this.model.name || !this.model.password) {
        return this.$message.error("用户名或密码不能为空");
      }
      const res = await this.axios.post("login", this.model);
      localStorage.token = res.data.token; //将token写入本地缓存中
      this.$router.push("/");
      this.$message.success("登录成功");
    }
```

现在前端有了token就得给所有请求之前加个请求头
axios里加个拦截器
```js
//前拦截器
http.interceptors.request.use(config => {
    //为所有的请求添加一个token 前面加Bearer是为了规范
    config.headers.Authorization ="Bearer " + localStorage.token
    return config
})
```
后端改接口，处理token,列表页为例
```js
    //列表接口
    router.get("/", async (req, res, next) => {
        const token = String(req.headers.authorization||'').split(" ").pop()//这里前端定义的请求头是大写，后端要小写 pop提取最后一个元素
        if(!token){
            //没有token报错
            return res.status(401).send({
                message: "请先登录"
            })
        }
        const {id} = jwt.verify(token,"sybsdz")//verify是校验，第一个参数是token，第二个是自己定义的那个秘钥，注意这时jwt的引用已经提到最上面了,这个id就是用户的id
        if(!id){
            //解密不出来id
            return res.status(401).send({
                message: "请先登录"
            })
        }
        req.user = await Admin.findById(id)//通过id去admin表里查，万一是假的呢，注意这里Admin的引入也提前到最开始了
        if(!req.user){
            //没有这个用户
            return res.status(401).send({
                message: "请先登录"
            })
        }
        console.log(req.user)
        await next()
    }, async (req, res) => {
        const queryOptions = {}
        //如果数据库中有关联字段，就可以用populate查出来,传进去什么字段，就会直接找对应字段id所属的集合的所有信息，而不仅仅是id了
        if (req.Model.modelName === "Category") {
            queryOptions.populate = "parent"
        }
        // queryOptions.populate = "parent"
        const items = await req.Model.find().setOptions(queryOptions)//查找所有数据，限制10条   
        res.send(items)//发送到客户端
    })
 ```
 前端在axios拦截器中判断，状态码是401就跳到登录页
 ```js
 import router from "./router"//先把路由引进来
 
 //后拦截器
http.interceptors.response.use(res => {
    return res //没问题就直接return
}, err => {
    if (err.response.data.message) {
        //console.log(err.response.data.message)报错的响应数据
        Vue.prototype.$message.error(err.response.data.message)//现在vue实例上有element，可以直接用$message这个弹出框
    }
    if(err.response.status=== 401 ){
        console.log(1)
        router.push("/login")//跳到登录页
    }
    return Promise.reject(err)//有问题就返回报错
})
```

现在去后端把判断token的中间件变成个模块
```js
    //登录授权中间件
    const auth = async (req, res, next) => {
        const token = String(req.headers.authorization||'').split(" ").pop()//这里前端定义的请求头是大写，后端要小写 pop提取最后一个元素
        if(!token){
            //没有token报错
            return res.status(401).send({
                message: "请先登录"
            })
        }
        const {id} = jwt.verify(token,"sybsdz")//verify是校验，第一个参数是token，第二个是自己定义的那个秘钥，注意这时jwt的引用已经提到最上面了,这个id就是用户的id
        if(!id){
            //解密不出来id
            return res.status(401).send({
                message: "请先登录"
            })
        }
        req.user = await Admin.findById(id)//通过id去admin表里查，万一是假的呢，注意这里Admin的引入也提前到最开始了
        if(!req.user){
            //没有这个用户
            return res.status(401).send({
                message: "请先登录"
            })
        }
        console.log(req.user)
        await next()
    }

	//在需要的地方直接用auth
    app.use("/admin/api/rest/:resource",auth,
        async (req, res, next) => {
            const ModelName = require("inflection").classify(req.params.resource)//转类名大小写，单复数
            // const Model = require(`../../models/${ModelName}`)
            //由于这样后面的中间件是拿不到这个Model的，所以要把他添加到req中
            req.Model = require(`../../models/${ModelName}`)
            next()
        }, router)
  ```
  但是现在图片上传没有加上token
  去main.js定义一个全局的加header方法 一定要写在new Vue前面
  ```js
  Vue.mixin({
    methods: {
        getAuthHeaders() {
            return {
                Authorization: "Bearer " + (localStorage.token || '')
            }
        }
    }
})
```
之后在页面上直接用就行
```html
        <el-upload
          class="avatar-uploader"
          :action="axios.defaults.baseURL + '/upload'"
          :headers="getAuthHeaders()"
          :show-file-list="false"
          :on-success="afterUpload"
        >
  ```