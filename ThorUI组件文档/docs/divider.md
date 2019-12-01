# divider
Divider分隔符：可设置占据高度，线条宽度，颜色等。

## 组件结构
``` html
<template>
	<view class="tui-divider" :style="{height:height+'rpx'}">
		<view class="tui-divider-line" :style="{width:width,background:getBgColor(gradual,gradualColor,dividerColor)}"></view>
		<view class="tui-divider-text" :style="{color:color,fontSize:size+'rpx',lineHeight:size+'rpx',background:bgcolor}">
			<slot></slot>
		</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiDivider",
		props: {
			//divider占据高度
			height: {
				type: Number,
				default: 100
			},
			//divider宽度，可填写具体长度，如400rpx
			width: {
				type: String,
				default: "100%"
			},
			//divider颜色，如果为渐变线条，此属性失效
			dividerColor: {
				type: String,
				default: "#e5e5e5"
			},
			//文字颜色
			color: {
				type: String,
				default: "#999"
			},
			//文字大小 rpx
			size: {
				type: Number,
				default: 24
			},
			//背景颜色，和当前页面背景色保持一致
			bgcolor: {
				type: String,
				default: "#fafafa"
			},
			//是否为渐变线条，为true，divideColor失效
			gradual: {
				type: Boolean,
				default: false
			},
			//渐变色值，to right ，提供两个色值即可，由浅至深
			gradualColor: {
				type: Array,
				default: ["#eee", "#ccc"]
			}
		},
		methods: {
			getBgColor: function(gradual, gradualColor, dividerColor) {
				let bgColor = dividerColor;
				if (gradual) {
					bgColor = "linear-gradient(to right," + gradualColor[0] + "," + gradualColor[1] + "," + gradualColor[1] + "," +
						gradualColor[0] + ")";
				}
				return bgColor;
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
	 "height" :divider占据高度,类型:"Number",默认值:100
	 "width" :divider宽度，可填写具体长度，如400rpx,类型:"String",默认值:"100%"
	 "dividerColor" : divider颜色，如果为渐变线条，此属性失效,类型:"String",默认值:"#e5e5e5"
	 "color" : 文字颜色,类型:"String",默认值:"#999"
	 "size" : 文字大小 rpx,类型:"Number",默认值:24
	 "bgcolor" :背景颜色，和当前页面背景色保持一致,类型:"String",默认值:"#fafafa"
	 "gradual" : 是否为渐变线条，为true，divideColor失效,类型:"Boolean",默认值:false
	 "gradualColor" : 渐变色值，to right ，提供两个色值即可，由浅至深,类型:"Array",默认值: ["#eee", "#ccc"]
	 
 methods:
   "getBgColor":线条颜色处理

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 