title: React state 生命周期初体验
author: 大白腿
tags:
  - react
categories:
  - react
date: 2020-06-18 20:15:00
---
```js
class Clock extends React.Component{
  //初始化
  constructor(props){
    //把this指向改成props
    super(props)
    //类似vue中的data，react里是state,初始化数据
    this.state = {
      time : new Date().toLocaleTimeString()
    }
  }
  render(){
    return(
      <div>
        <h1>{this.state.time}</h1>
      </div>
    )
  }
  //生命周期,组件渲染完成时的函数
  componentDidMount(){
    setInterval(()=>{
      //this.state.time = new Date().toLocaleTimeString()错误的
      //常规操作，类似小程序
      this.setState({
        time :new Date().toLocaleTimeString()
      })
    },1000)
  }
}
ReactDOM.render(
  <Clock />,
  document.querySelector("#root")
)
```