# loading
Loading 加载

## 组件结构
``` html
<template>
	<view class="tui-loading-init" v-if="visible">
		<view class="tui-loading-center"></view>
		<view class="tui-loadmore-tips">{{text}}</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiLoading",
		props: {
			text: {
				type: String,
				default: "正在加载..."
			},
			visible: {
				type: Boolean,
				default: false
			}
		}
	}
</script>
``` 

## 组件样式

``` css
... 此处省略n行
``` 

## 脚本说明

``` js
 props: 
	 "text" : 显示文本,类型:"String",默认值:"正在加载..."
	 "visible" : 是否显示,类型:"Boolean",默认值:false
	 
 methods:
   无

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 