title: 手机rem
author: 大白腿
tags:
  - js
categories:
  - js
date: 2020-05-24 12:42:00
---
```js
!function(n){
    var  e=n.document,
         t=e.documentElement,
         i=720,
         d=i/100,
         o="orientationchange"in n?"orientationchange":"resize",
         a=function(){
             var n=t.clientWidth||320;n>720&&(n=720);
             t.style.fontSize=n/d+"px"
         };
         e.addEventListener&&(n.addEventListener(o,a,!1),e.addEventListener("DOMContentLoaded",a,!1))
}(window);
```

华盖rem
```js
        <script>
            (function(d,c){
                var e=d.documentElement,
                b="resize",
                a=function(){
                    var f = window.innerWidth;
                    if(!f){return}
                    e.style.fontSize= (f/1440*100).toFixed(0)+"px"
                    e.style.overflowX="hidden"
                };
                if(!d.addEventListener){return}
                c.addEventListener(b,a,false);
                d.addEventListener("DOMContentLoaded",a,false);
                a()
            })(document,window);
        </script>
   ```