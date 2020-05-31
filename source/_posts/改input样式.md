title: 改input样式
author: 大白腿
tags:
  - css
categories:
  - css
date: 2020-05-24 12:57:00
---
```css
input[type="radio"] {
    position: absolute;
    clip: rect(0, 0, 0, 0);
    }
input[type="radio"] + label::before{
    content: " ";
    display: inline-block;
    vertical-align: bottom;
    width: 18px;
    height: 18px;
    margin-right: .4em;
    border-radius: 50%;
    background: url(../images/5.png) no-repeat;
    background-size: 100% 100%;
    }
input[type="radio"]:checked + label::before {
        content: " ";
        display: inline-block;
        vertical-align: bottom;
        width: 18px;
        height: 18px;
        margin-right: .4em;
        border-radius: 50%;
        background: url(../images/4.png) no-repeat;
        background-size: 100% 100%;
        }
   ```