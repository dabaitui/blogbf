title: React父传子数据传递
author: 大白腿
tags:
  - react
categories:
  - react
date: 2020-06-21 11:28:00
---
```jsx
class Fdom extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      isActive: true
    }
    //改变change事件的this指向
    this.change = this.change.bind(this)
  }
  change(){
    this.setState({
      isActive : !this.state.isActive
    })
  }
  render() {
    return (
      <div>
        <button onClick={this.change}>控制子元素显示</button>
        <Cdom isActive={this.state.isActive} />
      </div>
    )
  }
}
class Cdom extends React.Component {
  constructor(props) {
    super(props)
  }
  render() {
    let el = null;
    el = this.props.isActive ? 'active' : ''
    return (
      <div className={"none "+el}>
        子元素
      </div>
    )
  }
}
ReactDOM.render(
  <Fdom />,
  document.querySelector("#root")
)
```