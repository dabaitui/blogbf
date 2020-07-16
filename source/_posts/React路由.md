title: React路由
author: 大白腿
tags:
  - react
categories:
  - react
date: 2020-06-26 11:54:00
---
### 1.先安装路由（本身不自带）
```
cnpm i react-router-dom --save
```

### 2.基本使用
先引入
```
//BrowserRouter本名，改成Router名
import {BrowserRouter as Router,Link,Route} from "react-router-dom"
```
```js
function Home(){
  return(
    <div>
      <h1>home</h1>
    </div>
  )
}
function Me(){
  return(
    <div>
      <h1>me</h1>
    </div>
  )
}
function New(props){
  console.log(props)
  return(
    <div>
      <h1>New</h1>
    </div>
  )
}
class RouterApp extends React.Component{
  render(){
    let meObj = {
      pathname:'/me',//跳转的路径
      search:"?name=abc",//get请求的参数
      hash:"#abc",//设置的hash指，锚值
      state:{ //传入的数据
        msg:"yes"
      }
    }
    return(
      <div>
      //整体用Router包起来
      //basename 相当于子路由所有的路由都在/admin下
        <Router  basename="/admin">
          <div className="nav">
          	//点击的Link
            <Link to="/">home</Link>
            //可以传入个对象，hash和参数会自动拼接 replace直接替换路由，没有返回上一页
            <Link to={meObj} replace>me</Link>
            //动态路由
            <Link to="/new/123">new</Link>
          </div>
          //要渲染的组件  exact是严格匹配一般给/的path加上 component是要渲染的组件
          <Route path="/" exact component={Home}></Route>
          <Route path="/me" component={Me}></Route>
          //动态路由
          <Route path="/new/:id" component={New}></Route>
        </Router>
      </div>
    )
  }
}
ReactDOM.render(
  <RouterApp></RouterApp>,
  document.querySelector("#root")
)
```

![upload successful](/images/pasted-30.png)

![upload successful](/images/pasted-31.png)


### 高级路由
```
//Redirect重定向用到的,Switch路由指匹配第一个
import {BrowserRouter as Router,Link,Route,Redirect,Switch} from "react-router-dom"
```
```js
function LoginInfo(props){
  console.log(props)
  if(props.location.state.loginState === "success"){
    return <Redirect to="/admin"></Redirect>
  }else{
    return <Redirect to="/login"></Redirect>
  }
}
let FormCom = ()=>{
  let pathObj = {
    pathname : '/loginInfo',
    state:{
      loginState:"success"
    }
  }
  return(
    <div>
      <h1>表单</h1>
      <Link to={pathObj}>登录</Link>
    </div>
  )
}
class AppRouter extends React.Component{
  render(){
    return(
      <div>
        <Router>
          <Route path="/" exact component={()=>(<h1>首页</h1>)}></Route>
          <Route path="/form" exact component={FormCom}></Route>
          <Route path="/login" exact component={()=>(<h1>登录</h1>)}></Route>
          <Route path="/loginInfo" exact component={LoginInfo}></Route>
        </Router>
      </div>
    )
  }
}
ReactDOM.render(
  <AppRouter></AppRouter>,
  document.querySelector("#root")
)
```
```JS
//Switch路由指匹配第一个
class AppRouter extends React.Component{
  render(){
    return(
      <div>
        <Router>
          <Switch>
          <Route path="/" exact component={()=>(<h1>首页</h1>)}></Route>
          <Route path="/form" exact component={FormCom}></Route>
          <Route path="/login" exact component={()=>(<h1>登录</h1>)}></Route>
          <Route path="/loginInfo" exact component={LoginInfo}></Route>
          <Route path="/abc" exact component={()=>(<h1>abc1</h1>)}></Route>
          <Route path="/abc" exact component={()=>(<h1>abc323</h1>)}></Route>
          <Route path="/abc" exact component={()=>(<h1>abc</h1>)}></Route>
          <Route path="/abc" exact component={()=>(<h1>abc123</h1>)}></Route>
          </Switch>
        </Router>
      </div>
    )
  }
}
```
### js控制路由跳转
```js
class Abc extends React.Component{
  render(){
    return(
      <div>
        <button onClick={this.toHmoe}>去首页</button>
      </div>
    )
  }
  toHmoe = ()=>{
    console.log(this.props)
    this.props.history.push("/")
    //this.props.history.go(-1) 后退
  }
}
```