# tips
tips提示，默认居中显示

## 组件结构
``` html
<template>
	<view class="tui-tips-box" :class="[fixed?'tui-tips-fixed':'']">
		<image :src="imgUrl" class="tui-tips-icon" :style="{width:imgWidth+'rpx',height:imgHeight+'rpx'}"></image>
		<view class="tui-tips-content">
			<slot></slot>
		</view>
		<button class="tui-tips-btn" hover-class="tui-tips-btn-hover" :style="{width:btnWidth+'rpx'}" v-if="btnText"  @tap="handleClick">{{btnText}}</button>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiTips",
		props: {
			//是否垂直居中
			fixed: {
				type: Boolean,
				default: true
			},
			//图片地址，没有则不显示
			imgUrl: {
				type: String,
				default: ""
			},
			//图片宽度
			imgWidth: {
				type: Number,
				default: 200
			},
			//图片高度
			imgHeight:{
				type: Number,
				default: 200
			},
			//按钮宽度
			btnWidth:{
				type: Number,
				default: 200
			},
			//按钮文字，没有则不显示
			btnText:{
				type:String,
				default: ""
			}
		},
		methods: {
			handleClick(e) {
				this.$emit('click', {});
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
	 "fixed" : 是否垂直居中，默认 true
	 "imgUrl":图片地址，没有则不显示
	 "imgWidth":图片宽度，默认 200rpx
	 "imgHeight":图片高度，默认 200rpx
	 "btnWidth" :按钮宽度
	 "btnText" :按钮文字，没有则不显示
	 
 methods:
   "handleClick":按钮点击事件

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 