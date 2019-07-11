# keyboard-input
keyboard-input 数字键盘输入框，结合keyboard使用

## 组件结构
``` html
<template>
	<view class="tui-keyboard-input tui-pwd-box" :style="{background:bgcolor}">
		<view class="tui-inner-box">
			<view class="tui-input" :class="[inputvalue.length===4?'tui-margin-right':'']" :style="{fontSize:px(size),color:color,width:px(inputvalue.length===4?90:70)}"
			 v-for="(item,index) in inputvalue" :key="index">{{item}}</view>
		</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name:"KeyboardInput",
		props: {
			//背景颜色
			bgcolor: {
				type: String,
				default: "#fff"
			},
			size: {
				type: Number,
				default: 32
			},
			color: {
				type: String,
				default: "#333"
			},
			//输入框的值：数组格式，长度即为输入框个数
			inputvalue: {
				type: Array,
				default: ["", "", "", "", "", ""] //密码圆点 ●
			}
		},
		data() {
			return {

			};
		},
		methods: {
			px(num) {
				return uni.upx2px(num) +"px"
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
	 "bgcolor" : 输入框外层背景颜色,类型:"String",默认值:"#fff"
	 "size" : 输入框文字大小,类型:"Number",默认值:32upx
	 "color" :输入框文字颜色,类型:"String",默认值:"#333"
	 "inputvalue" :输入框的值：数组格式，长度即为输入框个数,类型:"Array",默认值:["", "", "", "", "", ""] //密码圆点 ●
	 
 methods:
   "px":upx转px,已经支持rpx

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 