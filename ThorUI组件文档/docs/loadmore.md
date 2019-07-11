# loadmore
loadmore 加载更多

## 组件结构
``` html
<template>
	<view class="tui-loadmore" v-if="visible">
		<view :class="['tui-loading-'+index, (index==3 && type)?'tui-loading-'+type:'']"></view>
		<view class="tui-loadmore-tips">{{text}}</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiLoadmore",
		props: {
			//显示文本
			text: {
				type: String,
				default: "正在加载..."
			},
			//是否可见
			visible: {
				type: Boolean,
				default: false
			},
			//loading 样式 ：1,2,3
			index: {
				type: Number,
				default: 1
			},
			//颜色设置，只有index=3时生效：primary，red，orange，green
			type: {
				type: String,
				default: ""
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
	 "index" : loading 样式 ：[1,2,3],类型:"Number",默认值:1
	 "type" : 颜色设置，只有index=3时生效：primary，red，orange，green,类型:"String",默认值:""
	 
 methods:
   无

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 