# numberbox
NumberBox 数字框:可设置步长，支持浮点数，支持调整样式

## 组件结构
``` html
<template>
	<view class="tui-numberbox-class tui-numberbox">
		<view class="tui-numbox-icon tui-icon-reduce " :class="[disabled || min>=value?'tui-disabled':'']" @tap="reduce"
		 :style="{color:iconcolor,fontSize:px(iconsize)}"></view>
		<input type="number" v-model="val" :disabled="disabled" @blur="blur" class="tui-num-input" :style="{color:color,fontSize:px(iconsize),background:bgcolor,height:px(height),width:px(width)}" />
		<view class="tui-numbox-icon tui-icon-plus" :class="[disabled || value>=max?'tui-disabled':'']" @tap="plus" :style="{color:iconcolor,fontSize:px(iconsize)}"></view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiNumberbox",
		props: {
			value: {
				type: Number,
				default: 1
			},
			//最小值
			min: {
				type: Number,
				default: 0
			},
			//最大值
			max: {
				type: Number,
				default: 100
			},
			//迈步大小 1 1.1 10...
			step: {
				type: Number,
				default: 1
			},
			//是否禁用操作
			disabled: {
				type: Boolean,
				default: false
			},
			//加减图标大小 rpx
			iconsize: {
				type: Number,
				default: 24
			},
			iconcolor: {
				type: String,
				default: "#333"
			},
			//input 高度
			height: {
				type: Number,
				default: 50
			},
			//input 宽度
			width: {
				type: Number,
				default: 90
			},
			//input 背景颜色
			bgcolor: {
				type: String,
				default: "#f2f2f2"
			},
			//input 字体颜色
			color: {
				type: String,
				default: "#333"
			}
		},
		computed: {
			val() {
				return this.value 
			}
		},
		data() {
			return {

			};
		},
		methods: {
			px(num) {
				return uni.upx2px(num) + "px"
			},
			getScale() {
				let scale = 1;
				//浮点型
				if (!Number.isInteger(this.step)) {
					scale = Math.pow(10, (this.step + '').split('.')[1].length)
				}
				return scale;
			},
			calcNum: function(type) {
				if (this.disabled) {
					return
				}
				const scale = this.getScale()
				let num = this.value * scale
				let step = this.step * scale
				if (type === 'reduce') {
					num -= step
				} else if (type === 'plus') {
					num += step
				}
				let value = num / scale
				if (value < this.min || value > this.max) {
					return
				}

				this.handleChange(value, type)
			},
			plus: function() {
				this.calcNum("plus")
			},
			reduce: function() {
				this.calcNum("reduce")
			},
			blur: function(e) {
				let value = e.detail.value
				if (value) {
					value = +value
					if (value > this.max) {
						value = this.max
					} else if (value < this.min) {
						value = this.min
					}
				} else {
					value = this.min
				}
				this.handleChange(value, "blur")
			},
			handleChange(value, type) {
				if (this.disabled) {
					return
				}
				this.$emit('change', {
					value: value,
					type: type
				})
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
	 "value" : 数字框值,类型:"Number",默认值:1
	 "min" : 最小值,类型:"Number",默认值:0
	 "max" : 最大值 ,类型:"Number",默认值:100
	 "step" : 迈步大小 1 1.1 10...,类型:"Number",默认值:1
	 "disabled" : 是否禁用操作,类型:"Boolean",默认值:false
	 "iconsize" : 加减图标大小 upx,类型:"Number",默认值:24
	 "iconcolor" : 图标颜色,类型:"String",默认值:"#333"
	 "height" : input 高度,类型:"Number",默认值:50
	 "width" : input 宽度,类型:"Number",默认值:90
	 "bgcolor" :input 背景颜色,类型:"Boolean",默认值:false
	 "color" : input 字体颜色,类型:"Boolean",默认值:false
	 
 methods:
   "px":upx转px
   "getScale":获取缩放倍数 ，（1.1=>10,1.11=>100）
   "calcNum":计算input值
   "plus":加号事件
   "reduce":减号事件
   "blur":失去焦点执行的事件
   "handleChange":input数值变化事件

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 