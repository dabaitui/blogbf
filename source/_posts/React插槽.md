title: React插槽
author: 大白腿
tags:
  - react
categories:
  - react
date: 2020-06-26 11:38:00
---
```js
//插槽
class ParentCom extends React.Component{
  constructor(props){
    super(props)
    console.log(props)
  }
  render(){
    return(
      <div>
        <h1>组件插槽</h1>
        {this.props.children}
      </div>
    )
  }
}
ReactDOM.render(
  <ParentCom>
    <h2>我是插进来的内容h2</h2>
    <h3>我是插进来的内容h3</h3>
    <h4>我是插进来的内容h4</h4>
  </ParentCom>,
  document.querySelector("#root")
)	
```


![upload successful](/images/pasted-29.png)