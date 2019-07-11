# time-axis
time-axis 时间轴，结合timeaxis-item使用

## 组件结构
``` html
<template>
	<view class="tui-timeaxis-class tui-time-axis">
		<slot></slot>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name:"tuiTimeAxis",
		data() {
			return {

			};
		}
	}
</script>
``` 

## 组件样式

``` css
<style>
	.tui-time-axis {
		padding-left: 20px;
		box-sizing: border-box;
		position: relative;
	}

	.tui-time-axis::before {
		content: " ";
		position: absolute;
		left: 0;
		top: 0;
		width: 1px;
		bottom: 0;
		border-left: 1px solid #ddd;
		-webkit-transform-origin: 0 0;
		transform-origin: 0 0;
		-webkit-transform: scaleX(0.5);
		transform: scaleX(0.5);
	}
</style>

``` 

## 脚本说明

``` js
 props: 
	 无
	 
 methods:
   无

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 