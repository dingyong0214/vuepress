# list-view
list-view 列表，结合list-cell使用

## 组件结构
``` html
<template>
	<view class="tui-list-view tui-view-class">
		<view class="tui-list-title" v-if="title">{{title}}</view>
		<view class="tui-list-content" :class="[unlined?'tui-border-'+unlined:'']">
			<slot></slot>
		</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiListView",
		props: {
			title: {
				type: String,
				default: ''
			},
			unlined: {
				type: String,
				default: '' //top,bottom,all
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
	 "title" : 列表title,类型:"String",默认值:""
	 "unlined" : 去掉线条，可传入[top,bottom,all],类型:"String",默认值:""
	 
 methods:
   无

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 