title: scss 样式穿透
author: 大白腿
tags:
  - css
  - scss
categories:
  - scss
date: 2020-05-24 15:09:00
---
解决swiper样式修改与scoped冲突的问题
```css
.case ::v-deep .swiper-pagination-bullet{
    width: 50px;
    opacity: 1;
    border-radius: 0;
    height: 2px;
    background: #000;
    transition: 0.3s;
}
```