# modal
Modal弹框:可设置按钮数，按钮样式，提示文字样式等，还可自定义弹框内容

## 组件结构
``` html
<template>
	<view>
		<view class="tui-modal-class tui-modal-box" :class="[show?'tui-modal-show':'']">
			<view v-if="!custom">
				<view class="tui-modal-title" v-if="title">{{title}}</view>
				<view class="tui-modal-content" :class="[title?'':'tui-mtop']" :style="{color:color,fontSize:px(size)}">{{content}}</view>
				<view class="tui-modalBtn-box" :class="[button.length>2?'tui-flex-column':'']">
					<block v-for="(item,index) in button" :key="index">
						<button class="tui-modal-btn" :class="['tui-'+(item.type || 'primary')+(item.plain?'-outline':''),button.length!=2?'tui-btn-width':'',button.length>2?'tui-mbtm':'',shape=='circle'?'tui-circle-btn':'']"
						 :hover-class="'tui-'+(item.plain?'outline':(item.type || 'primary'))+'-hover'" :data-index="index" @tap="handleClick">{{item.text || "确定"}}</button>
					</block>
				</view>
			</view>
			<view v-else>
				<slot></slot>
			</view>
		</view>
		<view class="tui-modal-mask" :class="[show?'tui-mask-show':'']" @tap="handleClickCancel"></view>

	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiModal",
		props: {
			//是否显示
			show: {
				type: Boolean,
				default: false
			},
			//标题
			title: {
				type: String,
				default: ""
			},
			//内容
			content: {
				type: String,
				default: ""
			},
			//内容字体颜色
			color: {
				type: String,
				default: "#999"
			},
			//内容字体大小
			size: {
				type: Number,
				default: 28
			},
			//形状 circle, square
			shape: {
				type: String,
				default: 'square'
			},
			button: {
				type: Array,
				default: function() {
					return [{
						text: "取消",
						type: "red",
						plain: true //是否空心
					}, {
						text: "确定",
						type: "red",
						plain: false
					}]
				}
			},
			//点击遮罩 是否可关闭
			maskClosable: {
				type: Boolean,
				default: true
			},
			//自定义弹窗内容
			custom: {
				type: Boolean,
				default: false
			}
		},
		data() {
			return {

			};
		},
		methods: {
			handleClick(e) {
				if (!this.show) return;
				const dataset = e.currentTarget.dataset;
				this.$emit('click', {
					index: Number(dataset.index)
				});
			},
			handleClickCancel() {
				if (!this.maskClosable) return;
				this.$emit('cancel');
			},
			px(num) {
				return uni.upx2px(num) + 'px'
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
	 "show" : 控制显示,类型:"Boolean",默认值:false
	 "title" : 标题,类型:"String",默认值:""
	 "content" : 详细内容,类型:"String",默认值:""
	 "color" : 详细内容字体颜色,类型:"String",默认值:"#999"
	 "size" : 详细内容字体大小upx,类型:"Number",默认值:28
	 "shape" : 按钮形状 circle(圆角), square(默认),类型:"String",默认值:"square"
	 "button" : 按钮,类型:"Array",默认值:
	            [{
					text: "取消",//按钮文本
					type: "red",//按钮样式类型  (primary,danger,red,warning,green,white,gray)
					plain: true //是否空心
				}, {
					text: "确定",
					type: "red",
					plain: false
				}]
	 "maskClosable" : 点击遮罩 是否可关闭,类型:"Boolean",默认值:true
	 "custom" : 自定义弹窗内容,类型:"Boolean",默认值:false	 
 methods:
   "handleClick":modal框按钮点击事件，非自定义内容时有效
   "handleClickCancel":关闭modal框
   "px":upx转px

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 