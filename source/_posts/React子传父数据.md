title: React子传父数据
author: 大白腿
tags:
  - react
categories:
  - react
date: 2020-06-21 11:50:00
---
```JS
class Fdom extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      data:null
    }
  }
  render() {
    return (
      <div>
        <h1>子给父传的数据:{this.state.data}</h1>
        //将传值方法给子组件传过去
        <Cdom setChildData={this.setChildData} />
      </div>
    )
  }
  //构建子给父传值的方法
  setChildData=(msg)=>{
    this.setState({
      data : msg
    })
  }
}
class Cdom extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      msg :'hello'
    }
    this.zouni = this.zouni.bind(this)
  }
  zouni(){
    console.log(this)
    this.props.setChildData(this.state.msg)
  }
  render() {
    return (
      <div>
        <button onClick={this.zouni}>走你</button>
        <button onClick={()=>{
          this.props.setChildData("走你2")
        }}>走你2</button>
      </div>
    )
  }
}
ReactDOM.render(
  <Fdom />,
  document.querySelector("#root")
)
```