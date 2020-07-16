title: uni-app接口封装
author: 大白腿
tags:
  - uni app
categories:
  - uni app
date: 2020-06-06 19:36:00
---
```js
import store from "../../store/index.js"
export default {
	common: {
		baseUrl: 'http://192.168.1.11:3000/api',
		data: {},
		header: {
			"Content-Type": "application/json",
			"Content-Type": "application/x-www-form-urlencoded",
		},
		method: "GET"
	},
	request(options = {}) {
		// uni.showLoading({
		//     title: '加载中'
		// });
		
		options.url = this.common.baseUrl + options.url;
		options.data = options.data || this.common.data;
		options.header = options.header || this.common.header;
		options.method = options.method || this.common.method;
		// 判断是否有token
		if(options.header.token){
			options.header.token = store.state.user.token
			if(!options.header.token){
				uni.showToast({
					title:"请先登录",
					icon:"none"
				})
				uni.navigateTo({
					url:"/pages/login/login"
				})
				return
			}
		}
		
		return new Promise((res, rej) => {
			uni.request({
				...options,
				success: (result) => {
					if (result.statusCode != 200) {
						return rej()
					}
					// setTimeout(function () {
					//     uni.hideLoading();
					// }, 1000);
					let data = result.data.data
					res(data)
				}
			})
		})
	}
}

```