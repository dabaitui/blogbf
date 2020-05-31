title: animation动画
author: 大白腿
tags:
  - css
categories:
  - css
date: 2020-05-24 12:37:00
---
```css
div
{
width:100px;
height:100px;
background:red;
position:relative;
animation:mymove 5s infinite;
-moz-animation:mymove 5s infinite; /* Firefox */
-webkit-animation:mymove 5s infinite; /* Safari and Chrome */
-o-animation:mymove 5s infinite; /* Opera */
animation-fill-mode:forwards;//动画结束后使用
}

@keyframes mymove
{
0%   {top:0px;}
25%  {top:200px;}
75%  {top:50px}
100% {top:100px;}
}
@-moz-keyframes mymove /* Firefox */
{
0%   {top:0px;}
25%  {top:200px;}
75%  {top:50px}
100% {top:100px;}
}

@-webkit-keyframes mymove /* Safari and Chrome */
{
0%   {top:0px;}
25%  {top:200px;}
75%  {top:50px}
100% {top:100px;}
}

@-o-keyframes mymove /* Opera */
{
0%   {top:0px;}
25%  {top:200px;}
75%  {top:50px}
100% {top:100px;}
}
```

animation-name	规定需要绑定到选择器的 keyframe 名称。。
animation-duration	规定完成动画所花费的时间，以秒或毫秒计。

animation-timing-function	规定动画的速度曲线。
取值：linear	动画从头到尾的速度是相同的。	测试
  	  ease	默认。动画以低速开始，然后加快，在结束前变慢。	测试
  	  ease-in	动画以低速开始。	测试
  	  ease-out	动画以低速结束。	测试
  	  ease-in-out	动画以低速开始和结束。	测试
  	  cubic-bezier(n,n,n,n)	在 cubic-bezier 函数中自己的值。可能的值是从 0 到 1 的数值。

animation-delay	规定在动画开始之前的延迟。
animation-iteration-count	规定动画应该播放的次数。
animation-direction	规定是否应该轮流反向播放动画。
animation-fill-mode:forwards 动画结束后应用