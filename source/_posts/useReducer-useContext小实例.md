title: useReducer+useContext小实例
author: 大白腿
tags:
  - react
  - hooks
categories:
  - react
date: 2020-06-30 20:31:00
---
```js
//botton
import React,{useContext} from 'react'
import {ColorContext,UPDATE_COlOR} from './color'
function Button(){
    const {dispatch} = useContext(ColorContext) //在需要使用变量时引入ColorContext,获取共享状态的值
    return(
        <div>
            <button onClick={()=>{dispatch({type:UPDATE_COlOR,color:"red"})}}>红</button>
            <button onClick={()=>{dispatch({type:UPDATE_COlOR,color:"yellow"})}}>黄</button>
        </div>
    )
}

export default Button
```
```js
//showArea
import React ,{useContext} from 'react'
import {ColorContext} from './color'

function ShowArea() {
    const {color} = useContext(ColorContext) //在需要使用变量时引入ColorContext,获取共享状态的值
    return (
        <div style={ {color:color} }>
            颜色
        </div>
    )
}


export default ShowArea
```
```js
///color
import React,{createContext,useReducer} from 'react'


export const ColorContext = createContext({}) //构建color组件的上下文

export const UPDATE_COlOR = 'UPDATE_COlOR'//定义常量

export const reducer = (state,action)=>{
    switch(action.type){
        case UPDATE_COlOR:
            return action.color
        default:
            return state
    }
}

export const Color = (props)=>{
    const [color,dispatch] = useReducer(reducer,"blue") //跟usestate有点像,传入两个值reducer和初始值
    return (
        <ColorContext.Provider value={{color,dispatch}}>
            {props.children} {/* 渲染子组件 */}
        </ColorContext.Provider>
    )
}
```
```js
//example6
import React from 'react'
import ShowArea from './showArea'
import Button from './Button'
import { Color } from './color'

function Example6() {
    return (
        <div>
            <Color>
                <ShowArea></ShowArea>
                <Button></Button>
            </Color>
        </div>
    )
}

export default Example6
```

![upload successful](/images/pasted-38.png)