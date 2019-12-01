# Fab
悬浮按钮:可设置left，right，bottom值，可设置大小，颜色等，具体参考文档。拓展出来的按钮不应多于6个，否则违反了作为悬浮按钮的快速、高效的原则。

## 组件结构
``` html
<template>
	<view @touchmove.stop.prevent>
		<view class="tui-fab-box" :class="{'tui-fab-right':!left || (left && right)}" :style="{left:getLeft(),right:getRight(),bottom:bottom+'rpx'}">
			<view class="tui-fab-btn" :class="{'tui-visible':isOpen,'tui-fab-hidden':hidden}">
				<view class="tui-fab-item-box" :class="{'tui-fab-item-left':left && !right && item.imgUrl}" v-for="(item,index) in btnList"
				 :key="index" @tap.stop="handleClick(index)">
					<view :class="[left && !right?'tui-text-left':'tui-text-right']" v-if="item.imgUrl" :style="{fontSize:item.fontSize+'rpx',color:item.color}">{{item.text || ""}}</view>
					<view class="tui-fab-item" :style="{width:width+'rpx',height:height+'rpx',background:item.bgColor || bgColor,borderRadius:radius}">
						<view class="tui-fab-title" v-if="!item.imgUrl" :style="{fontSize:item.fontSize+'rpx',color:item.color}">{{item.text || ""}}</view>
						<image :src="item.imgUrl" class="tui-fab-img" v-else :style="{width:item.imgWidth+'rpx',height:item.imgHeight+'rpx'}"></image>
					</view>
				</view>
			</view>
			<view class="tui-fab-item" :class="{'tui-active':isOpen}" :style="{width:width+'rpx',height:height+'rpx',borderRadius:radius,background:bgColor,color:color}"
			 @tap.stop="handleClick(-1)">
				<view class="tui-fab-icon tui-icon-plus"></view>
			</view>
		</view>
		<view class="tui-fab-mask" :class="{'tui-visible':isOpen}" @tap="handleClickCancel"></view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	//拓展出来的按钮不应多于6个，否则违反了作为悬浮按钮的快速、高效的原则
	export default {
		name: "tuiFab",
		props: {
			//rpx 为0时值为auto
			left: {
				type: Number,
				default: 0
			},
			//rpx 当为0时且left不为0，值为auto
			right: {
				type: Number,
				default: 80
			},
			//rpx bottom值
			bottom: {
				type: Number,
				default: 100
			},
			//默认按钮 宽度 rpx
			width: {
				type: Number,
				default: 108
			},
			//默认按钮 高度 rpx
			height: {
				type: Number,
				default: 108
			},
			//圆角值
			radius: {
				type: String,
				default: "50%"
			},
			//默认按钮背景颜色
			bgColor: {
				type: String,
				default: "#5677fc"
			},
			//字体颜色
			color: {
				type: String,
				default: "#fff"
			},
			//拓展按钮
			// bgColor: "#5677fc",
			// //图标/图片地址
			// imgUrl: "/static/images/fab/fab_reward.png",
			// //图片高度 rpx
			// imgHeight: 60,
			// //图片宽度 rpx
			// imgWidth: 60,
			// //名称
			// text: "名称",
			// //字体大小
			// fontSize: 30,
			// //字体颜色
			// color: "#fff"
			btnList: {
				type: Array,
				default () {
					return []
				}
			},
			//点击遮罩 是否可关闭
			maskClosable: {
				type: Boolean,
				default: false
			}
		},
		data() {
			return {
				isOpen: false,
				hidden: true,
				timer: null
			};
		},
		methods: {
			getLeft() {
				let val = "auto"
				if (this.left && !this.right) {
					val = this.left + 'rpx'
				}
				return val
			},
			getRight() {
				let val = this.right + 'rpx'
				if (this.left && !this.right) {
					val = "auto"
				}
				return val
			},
			handleClick: function(index) {
				this.hidden = false
				clearTimeout(this.timer)
				if (index == -1 && this.btnList.length) {
					this.isOpen = !this.isOpen
				} else {
					this.$emit("click", {
						index: index
					})
					this.isOpen = false
				}
				if (!this.isOpen) {
					this.timer = setTimeout(() => {
						this.hidden = true
					}, 200)
				}
			},
			handleClickCancel: function() {
				if (!this.maskClosable) return;
				this.isOpen = false
			}
		},
		beforeDestroy() {
			clearTimeout(this.timer)
			this.timer = null
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
	 "left" :left值，为0时值为auto，单位rpx(下同)，类型:"Number"，默认值:0	
	 "right" :right值，当为0时且left不为0，值为auto，类型:"Number",默认值:80	
	 "bottom" :bottom值，类型:"Number"，默认值：100
	 "width":默认按钮宽度,类型:"Number"，默认值:108
	 "height":默认按钮高度,类型:"Number"，默认值:108
	 "radius":圆角值，类型:"String",默认值:"50%"
	 "bgColor":默认按钮背景颜色，类型:"String",默认值:"#5677fc"
	 "color":字体颜色，类型:"String",默认值:"#fff"
	 "btnList":拓展按钮列表，类型:"Array",默认值:"[]"
	          [
				 //背景颜色
	            bgColor: "#5677fc",
	            //图标/图片地址
	            imgUrl: "/static/images/fab/fab_reward.png",
	            //图片高度 rpx
	            imgHeight: 60,
	            //图片宽度 rpx
	            imgWidth: 60,
	            //名称
	            text: "名称",
	            //字体大小
	            fontSize: 30,
	            //字体颜色
	            color: "#fff"
			]
	 "maskClosable":点击遮罩 是否可关闭，类型:"Boolean",默认值:false
	 
 methods:
   "handleClick":按钮点击事件，当有扩展按钮时，默认按钮点击只做【打开/关闭】扩展按钮操作
   "handleClickCancel":关闭扩展按钮，遮罩事件

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 

## 预览图

![](https://thorui.cn/img/V140/3.png)