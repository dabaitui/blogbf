title: jq平滑锚点过渡
author: 大白腿
tags:
  - js
  - jq
categories:
  - jq
date: 2020-05-24 12:54:00
---
```js
$('.aaa').click(function () {
    $('html, body').animate({
        scrollTop: $($.attr(this, 'href')).offset().top
    }, 800);
    return false;
});
```