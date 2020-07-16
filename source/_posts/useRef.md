title: useRef获取dom
author: 大白腿
tags:
  - react
  - hooks
categories:
  - react
date: 2020-07-01 20:43:00
---
```js
import React,{useRef} from 'react'
//用useRef获取dom
function Example8(){
    const inputEl = useRef()
    const showInput = ()=>{
        console.log(inputEl)//获取input的dom元素
        inputEl.current.value = 'hellow'
    }
    return(
        <div>
            <input ref={inputEl} type="text" />
            <button onClick={showInput}>展示</button>
        </div>
    )
}


export default Example8
```