# card
Card 卡片

## 组件结构
``` html
<template>
	<view class="tui-card-class tui-card" :class="[full?'tui-card-full':'',border?'tui-card-border':'']" @tap="handleClick"
	 @longtap="longTap">
		<view class="tui-card-header" :class="{'tui-header-line':header.line}" :style="{background:header.bgcolor || '#fff'}">
			<view class="tui-header-left">
				<image :src="image.url" class="tui-header-thumb" :class="{'tui-thumb-circle':image.circle}" mode="widthFix" v-if="image.url"
				 :style="{height:px(image.height || 60),width:px(image.width || 60)}"></image>
				<text class="tui-header-title" :style="{fontSize:px(title.size || 30),color:(title.color || '#7A7A7A')}" v-if="title.text">{{title.text}}</text>
			</view>
			<view class="tui-header-right" :style="{fontSize:px(tag.size || 24),color:(tag.color || '#b2b2b2')}" v-if="tag.text">
				{{tag.text}}
			</view>
		</view>
		<view class="tui-card-body">
			<slot name="body"></slot>
		</view>
		<view class="tui-card-footer">
			<slot name="footer"></slot>
		</view>
	</view>
</template>

``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiCard",
		props: {
			//是否铺满
			full: {
				type: Boolean,
				default: false
			},
			image: {
				type: Object,
				default: {
					url: "", //图片地址
					height: 60, //图片高度
					width: 60, //图片宽度
					circle: false
				}
			},
			//标题
			title: {
				type: Object,
				default: {
					text: "", //标题文字
					size: 30, //字体大小
					color: "#7A7A7A" //字体颜色
				}
			},
			//标签，时间等
			tag: {
				type: Object,
				default: {
					text: "", //标签文字
					size: 24, //字体大小
					color: "#b2b2b2" //字体颜色
				}
			},
			header: {
				type: Object,
				default: {
					bgcolor: "#fff", //背景颜色
					line: false //是否去掉底部线条
				}
			},
			//是否设置外边框
			border: {
				type: Boolean,
				default: false
			},
			index: {
				type: Number,
				default: 0
			}
		},
		methods: {
			handleClick() {
				this.$emit('click', {
					index: this.index
				});
			},
			longTap() {
				this.$emit('longclick', {
					index: this.index
				});
			},
			px(num) {
				return uni.upx2px(num) + "px"
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
	 "full" : 是否铺满宽度,类型:"Boolean",默认值:false
	 "image" :图片，头像等， 类型:"Object",默认值:
	            {
					url: "", //图片地址
					height: 60, //图片高度
					width: 60, //图片宽度
					circle: false //是否圆角
				}
	 "title" :标题,类型:"Object",默认值:
			  {
				text: "", //标题文字
				size: 30, //字体大小
				color: "#7A7A7A" //字体颜色
			 }
	 "tag":标签，时间等,类型:"Object",默认值:
			 {
				text: "", //标签文字
				size: 24, //字体大小
				color: "#b2b2b2" //字体颜色
			 }
	 "header":头部样式，类型:"Object",默认值:
			 {
				bgcolor: "#fff", //背景颜色
				line: false //是否去掉底部线条
			 }
	 "border":是否设置外边框,类型:"Boolean",默认值:false
	 "index":卡片索引,类型:"Number",默认值:0
	 
 methods:
   "handleClick":点击事件
   "longTap":长按事件
   "px":upx转换为px,后续会移除

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 