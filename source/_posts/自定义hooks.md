title: 自定义hooks
author: 大白腿
tags:
  - react
  - hooks
categories:
  - react
date: 2020-07-01 21:10:00
---
```js
import React ,{ useState , useEffect , useCallback } from 'react'
//监听窗口缩放实例

//自定义hooks函数,必须use开头
function useWindowSize(){
    //用useState记录大小，和改变大小的方法
    const [size,setSize] = useState({
        width:document.documentElement.clientWidth,
        height:document.documentElement.clientHeight,
    })
    //定义尺寸改变后执行的方法 useCallback缓存方法，利于优化
    const onResize = useCallback(()=>{
        setSize({
            width:document.documentElement.clientWidth,
            height:document.documentElement.clientHeight,
        })
    },[])
    //初始化方法
    useEffect(()=>{
        window.addEventListener("resize",onResize)
        //离开时销毁
        return ()=>{
            window.removeEventListener("resize",onResize)
            console.log("溜了溜了")
        }
    },[])

    return size
}

function Example6(){
    const size = useWindowSize()
    return(
        <div>
            <h1>{size.width}*{size.height}</h1>
        </div>
    )
}


export default Example6
```