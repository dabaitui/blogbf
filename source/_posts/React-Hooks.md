title: React Hooks
author: 大白腿
tags:
  - react
  - hooks
categories:
  - react
date: 2020-06-28 21:10:00
---
### useState，useEffect初体验
```js
import React, { useState, useEffect } from 'react'
import { BrowserRouter as Router, Link, Route } from "react-router-dom"
function Index() {
    useEffect(() => {
        console.log("useEffect index")
        return ()=>{
            //解绑,相当于WillUnmount
            console.log("溜了溜了")
        }
    },[])  //[]里可以传参数，表示只要数组内的内容变化才会解绑，直接[]就代表组件被销毁的时候执行
    return (
        <div>
            <h1>index</h1>
        </div>
    )
}
function About() {
    useEffect(() => {
        console.log("useEffect about")
    })
    return (
        <div>
            <h1>about</h1>
        </div>
    )
}
function Example() {
    //useState 会返回一对值：当前状态和一个让你更新它的函数
    const [count, setCount] = useState(0)
    //useEffect  相当于DidMount,DidUpdate,WillUnmount的结合体
    useEffect(() => {
        console.log("useEffect" + count)
    })
    return (
        <div>
            <p>click {count}</p>
            <button onClick={() => { setCount(count + 1) }}>click</button>
            <Router>
                <div>
                    <Link to="/">index</Link>
                    <Link to="/about">about</Link>
                </div>
                <div>
                    <Route path="/" exact component={Index}></Route>
                    <Route path="/about" component={About}></Route>
                </div>
            </Router>
        </div>
    )
}

export default Example
```