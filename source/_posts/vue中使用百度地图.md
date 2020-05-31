title: vue中使用百度地图
author: 大白腿
tags:
  - vue
categories:
  - vue
date: 2020-05-24 15:19:00
---
```
<script type="text/javascript" src="https://api.map.baidu.com/api?v=2.0&ak=nwNW4rgxKCm6cGYkSIPsezRjZ0vOsZyB"></script>
```
!!!可以引完js后在
```js
  methods: {
    createMap() {
		//生成器的代码  
	}
},
  mounted() {
    this.createMap();
  }
  ```
也要创建vue.config.js
```js
module.exports = {
    configureWebpack: {
      externals: {
        "BMap": "BMap"
      }
    }
  }
  ```
  正常方式
1.html引入
```
<script type="text/javascript" src="https://api.map.baidu.com/api?v=2.0&ak=nwNW4rgxKCm6cGYkSIPsezRjZ0vOsZyB"></script>
```
2.创建vue.config.js
```js
module.exports = {
    configureWebpack: {
      externals: {
        "BMap": "BMap"
      }
    }
  }
  ```
3.
```html
<div id="map" style="height:300px" class="map"></div>
```
```js
  methods: {
    createMap() {
      /* eslint-disable */
      // 创建Map实例
      var map = new BMap.Map("map");
      var point = new BMap.Point(123.409893,41.802065);
    //   map.centerAndZoom(point, 15);
      var marker = new BMap.Marker(point); // 创建标注
      map.addOverlay(marker);
      // 初始化地图,设置中心点坐标和地图级别
      map.centerAndZoom(new BMap.Point(123.410459, 41.802078), 18);
      //添加地图类型控件
      map.addControl(
        new BMap.MapTypeControl({
          mapTypes: [BMAP_NORMAL_MAP, BMAP_HYBRID_MAP]
        })
      );
      // 设置地图显示的城市 此项是必须设置的
      map.setCurrentCity("沈阳");
      //开启鼠标滚轮缩放
      map.enableScrollWheelZoom(true);
      /* eslint-enable */
    }
  },
  mounted() {
    this.createMap();
  }
```