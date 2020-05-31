title: 去掉number后面的箭头
author: 大白腿
tags:
  - css
categories:
  - css
date: 2020-05-24 12:34:00
---
```css
input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
  }
  input[type="number"] {
    -moz-appearance: textfield;
  }
```