title: vue滚动到某处执行
author: 大白腿
tags:
  - vue
categories:
  - vue
date: 2020-05-24 15:00:00
---
获取元素距顶的高
```
<div class="" ref="cs"></div>
this.$refs.cs.getBoundingClientRect().top
```
例子
```
  toscoll() {
      this.gao = this.$refs.cs.getBoundingClientRect().top;
      console.log(this.gao);
      if(this.gao<=600){
      }
    }
  mounted() {
    window.addEventListener('scroll', this.toscoll)//启动
  },
  //销毁
    destroyed(){
     window.removeEventListener("scroll", this.toscroll);
  }
  ```