# timeaxis-item
timeaxis-item 时间轴item，结合time-axis使用

## 组件结构
``` html
<template>
	<view class="timeaxis-item-class tui-timeaxis-item">
		<slot name="content"></slot>
		<view class="tui-node" :style="{background:bgcolor}">
			<slot name="node"></slot>
		</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiTimeaxisItem",
		props: {
			//节点背景色
			bgcolor: {
				type: String,
				default: "#fafafa"
			}
		},
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
	.tui-timeaxis-item {
		position: relative;
		width: 100%;
		display: flex;
		justify-content: center;
		flex-direction: column;
		margin-bottom: 25px;
	}

	.tui-node {
		position: absolute;
		top: 0;
		left: -20px;
		/* padding: 3px 0; */
		transform-origin: 0;
		transform: translateX(-50%);
		display: flex;
		align-items: center;
		justify-content: center;
		z-index: 99;
		background: #fafafa;
		font-size: 24upx;
	}
</style>
``` 

## 脚本说明

``` js
 props: 
	 "bgcolor":节点背景色,类型："String"，默认值："#fafafa"
	 
 methods:
   无

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 