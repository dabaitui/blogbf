title: Redux
author: 大白腿
tags:
  - react
categories:
  - react
date: 2020-06-26 17:29:00
---

![upload successful](/images/pasted-32.png)


### 安装

```
npm i redux --save
```

### 引入
```
import Redux,{createStore} from "redux" //将创作仓库的createStore方法解构出来
```
```js
//默认值num=0
const reducer = function (state = { num: 0 }, action) {
    switch (action.type) {
        case "add":
            state.num++;
            break;
        case "dec":
            state.num--
            break;
        default:
            break;
    }
    //最好返回一个全新的数据，可以先解构再创建
    return { ...state }
}
//构建仓库，之后丢一个函数进去
const store = createStore(reducer)
console.log(store)
function add() {
    //通过仓库的方法dispatch进行修改数据
    store.dispatch({ type: "add" })
    console.log(store.getState().num)
}
function dec() {
    store.dispatch({ type: "dec" })
}
//函数式计数器
const Counter = function (props) {
    return (
        <div>
            //从仓库中获取数据
            <h1>计数数量：{store.getState().num}</h1>
            <button onClick={dec}>-</button>
            <button onClick={add}>+</button>
        </div>
    )
}
ReactDOM.render(
    <Counter></Counter>,
    document.querySelector("#root")
)

//store的监听数据的变化，重新渲染
store.subscribe(()=>{
    ReactDOM.render(
        <Counter></Counter>,
        document.querySelector("#root")
    )
})
```