title: useMemo
author: 大白腿
tags:
  - react
  - hooks
categories:
  - react
date: 2020-06-30 20:59:00
---
```js
import React,{useState,useMemo} from 'react'

function Example4(){
    const [xiaohong,setXiaoHong] = useState("小红在吃饭")
    const [dahong,setDaHong] = useState("大红在睡觉")
    return(
        <div>
            <button onClick={()=>{
                setXiaoHong(new Date().getTime())
            }}>小红</button>
            <button onClick={()=>{
                setDaHong(new Date().getTime()+"啦啦啦")
            }}>大红</button>
            <ChildrenCom name={xiaohong}>{dahong}</ChildrenCom>
        </div>
    )
}

function ChildrenCom({name,children}){
    function changeXiaoHong(name){
        console.log("xiaohong!!!!!!!!!!!!")
        return name+"小红他来了"
    }
    const actionXiaoHong =useMemo(()=>changeXiaoHong(name),[name])//接收两个参数第一个是方法，第二个是当什么改变时执行，跟useEffect像，这里是name改变时才再次执行此方法
    return(
        <div>
            <div>{actionXiaoHong}</div>
            <div>{children}</div>
        </div>
    )
}

export default Example4
```