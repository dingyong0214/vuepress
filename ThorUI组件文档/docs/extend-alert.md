# Alert
Alert弹框

## 组件结构
``` html
<template>
	<view>
		<view class="tui-alert-class tui-alert-box" :class="[show?'tui-alert-show':'']">
			<view class="tui-alert-content" :style="{fontSize:size+'rpx',color:color}">
				<slot></slot>
			</view>
			<view class="tui-alert-btn" :style="{color:btnColor}" hover-class="tui-alert-btn-hover" :hover-stay-time="150"
			 @tap.stop="handleClick">{{btnText}}</view>
		</view>
		<view class="tui-alert-mask" :class="[show?'tui-alert-mask-show':'']" @tap.stop="handleClickCancel"></view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name:"tuiAlert",
		props: {
			//控制显示
			show: {
				type: Boolean,
				default: false
			},
			//提示信息字体大小
			size: {
				type: Number,
				default: 30
			},
			//提示信息字体颜色
			color: {
				type: String,
				default: "#333"
			},
			//按钮字体颜色
			btnColor: {
				type: String,
				default: "#EB0909"
			},
			btnText:{
				type: String,
				default: "确定"
			},
			//点击遮罩 是否可关闭
			maskClosable: {
				type: Boolean,
				default: false
			}
		},
		methods: {
			handleClick(e) {
				if (!this.show) return;
				this.$emit('click', {});
			},
			handleClickCancel() {
				if (!this.maskClosable) return;
				this.$emit('cancel');
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
	 "show" : 控制显示
	 "size":提示信息字体大小
	 "color":提示信息字体颜色
	 "btnColor":按钮字体颜色
	 "btnText" :按钮显示文本
	 "maskClosable" :点击遮罩 是否可关闭，默认 false
	 
 methods:
   "handleClick":按钮点击事件
   "handleClickCancel":遮罩点击事件

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 