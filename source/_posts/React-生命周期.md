title: React 生命周期
author: 大白腿
tags:
  - react
categories:
  - react
date: 2020-06-25 15:40:00
---
```js
class ComLife extends React.Component{
  constructor(props){
    super(props)
    this.state = {
      msg : "Hello  World"
    }
    console.log("constructor构造函数")
  }
  //开始渲染
  componentWillMount(){
    console.log("componentWillMount组件将要渲染")
  }
  //渲染完毕
  componentDidMount(){
    console.log("componentDidMount组件渲染完毕")
  }
  //接收新的数据
  componentWillReceiveProps(){
    console.log("componentWillReceiveProps组件将要接收新的state和props")
  }
  //组件将要更新
  componentWillUpdate(){
    console.log("componentWillUpdate组件将要更新")
  }
  //组件更新完成
  componentDidUpdate(){
    console.log("componentDidUpdate组件更新完成")
  }
  //移除
  componentWillUnmount(){
    console.log("componentWillUnmount移除")
  }
  render(){
    console.log("render渲染函数")
    return(
      <div>
        <h1>{this.state.msg}</h1>
        <button onClick={this.changeMsg}>组件更新</button>
      </div>
    )
  }
  changeMsg = ()=>{
    this.setState({
      msg : "滚"
    })
  }
}
ReactDOM.render(
  <ComLife />,
  document.querySelector("#root")
)
```


![upload successful](/images/pasted-27.png)



![upload successful](/images/pasted-28.png)