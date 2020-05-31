title: uni app 获取视口高
author: 大白腿
tags:
  - uni app
categories:
  - uni app
date: 2020-05-24 16:32:00
---
```
			uni.getSystemInfo({
				success: (res) => {
					this.swiperHeight = res.windowHeight - uni.upx2px(80) - this.getSwiperHeight()
				}
			})
      ```