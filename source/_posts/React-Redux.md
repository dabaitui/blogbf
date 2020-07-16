title: React-Redux
author: 大白腿
tags:
  - react
categories:
  - react
date: 2020-06-27 10:46:00
---
### 安装
```
npm i react-redux --save
```
```
import { createStore } from "redux"
import { Provider,connect } from "react-redux"
```

```js
class Counter extends React.Component{
    render(){
        //计数,通过stroe的state传给props，直接通过props就可以获取state数据
        const value = this.props.value
        // 将修改数据事件的方法传到props
        const onAdd = this.props.onAdd
        return(
            <div>
                <h1>计数:{value}</h1>
                <button onClick={onAdd}>+</button>
            </div>
        )
    }
}


//定义动作
const addAction = {
    type:"add"
}


function reducer(state={num:0},action){
    switch(action.type){
        case "add":
            state.num++
            break;
        default:
            break;
    }
    return {...state}
}
//创造仓库
const store = createStore(reducer)
//将state映射到props
function mapStateToProps(state){
    return{
        value:state.num
    }
}
//将修改state数据方法映射到props
function mapDispatchToProps(dispatch){
    return{
        //传入动作
        onAdd :()=>{dispatch(addAction)}
    }
}
//将上面两个方法映射到组件上，形成新的组件
const AppCounter = connect(
    mapStateToProps,
    mapDispatchToProps
)(Counter)//传入组件，形成新的组件
ReactDOM.render(
    <Provider store={store}>//最大的根组件
        <AppCounter></AppCounter>
    </Provider>,
    document.querySelector("#root")
)

```


![upload successful](/images/pasted-33.png)