title: useContext
author: 大白腿
tags:
  - react
  - hooks
categories:
  - react
date: 2020-06-29 20:41:00
---
```js
import React, { useState , createContext , useContext } from 'react'
const CountContext = createContext()//构建上下文组件
function Child(){
    let count = useContext(CountContext) //传入共享组件的名、
    return(
        <div>
            {count}
        </div>
    )
}
function Example2() {
    const [count, setCount] = useState(0)
    return (
        <div>
            <p>click {count}</p>
            <button onClick={() => { setCount(count + 1) }}>click</button>
            <CountContext.Provider value={count}>{/* value 里放的是要传递的数据 */}
                <Child></Child>
            </CountContext.Provider>
        </div>
    )
}

export default Example2
```