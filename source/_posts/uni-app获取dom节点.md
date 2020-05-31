title: uni app获取dom节点
author: 大白腿
tags:
  - uni app
categories:
  - uni app
date: 2020-05-24 16:19:00
---
```js
		onReady() {
			let view = uni.createSelectorQuery().select(".home_data");
			view.boundingClientRect(data => {
				console.log(data)
			}).exec();
		},
   ```