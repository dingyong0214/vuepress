# uni-app组件基本使用

如果不熟悉，可去[vuejs](https://cn.vuejs.org/)官网查看文档。

## 引入组件
``` js
<script>
	import tuiComponent from "@/components/component/component"
	export default {
		components:{
			tuiComponent
		},
		data() {
			return {
			}
		},
		methods: {
		}
	}
</script>
```

## 使用组件

``` html
<tui-component :show="show" :color="color" :size="size" :is-cancel="isCancel" @click="click"></tui-component>
```
 
 其中 :show="show" :color="color" :size="size" :is-cancel="isCancel" 部分为props，@click为组件绑定事件
 
 
 # 微信小程序组件基本使用

## 在页面.json文件中引入

``` js
  "usingComponents": {
    "tui-list-cell":"/components/list-cell/list-cell",
    "tui-toast":"/components/toast/toast"
  }
```

## 使用组件

``` html
<tui-list-cell arrow="{{true}}" unlined="{{true}}" hover="{{false}}"></tui-list-cell>
```


