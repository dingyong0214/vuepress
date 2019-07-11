# actionsheet
操作菜单:可加入提示信息，可单独设置字体样式。

## 组件结构
``` html
<template>
	<view>
		<view class="tui-actionsheet-class tui-actionsheet" :class="[show?'tui-actionsheet-show':'']">
			<view class="tui-tips" :style="{fontSize:px(size),color:color}" v-if="tips">
				{{tips}}
			</view>
			<view :class="[isCancel?'tui-operate-box':'']">
				<block v-for="(item,index) in itemList" :key="index">
					<view class="tui-actionsheet-btn tui-actionsheet-divider" :class="[(!isCancel && index==itemList.length-1)?'tui-btn-last':'']"
					 hover-class="tui-actionsheet-hover" :hover-stay-time="150" :data-index="index" :style="{color:item.color || '#1a1a1a'}"
					 @tap="handleClickItem">{{item.text}}</view>
				</block>
			</view>
			<view class="tui-actionsheet-btn tui-actionsheet-cancel" hover-class="tui-actionsheet-hover" :hover-stay-time="150"
			 v-if="isCancel" @tap="handleClickCancel">取消</view>
		</view>
		<view class="tui-actionsheet-mask" :class="[show?'tui-mask-show':'']" @tap="handleClickMask"></view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiActionsheet",
		props: {
			//点击遮罩 是否可关闭
			maskClosable: {
				type: Boolean,
				default: true
			},
			//显示操作菜单
			show: {
				type: Boolean,
				default: false
			},
			//菜单按钮数组，自定义文本颜色，红色参考色：#e53a37
			itemList: {
				type: Array,
				default: [{
					text: "确定",
					color: "#1a1a1a"
				}]
			},
			//提示文字
			tips: {
				type: String,
				default: ""
			},
			//提示文字颜色
			color: {
				type: String,
				default: "#9a9a9a"
			},
			//提示文字大小
			size: {
				type: Number,
				default: 26
			},
			//是否需要取消按钮
			isCancel: {
				type: Boolean,
				default: true
			}
		},
		methods: {
			px(num) {
				return uni.upx2px(num) + "px"
			},
			handleClickMask() {
				if (!this.maskClosable) return;
				this.handleClickCancel();
			},
			handleClickItem(e) {
				if (!this.show) return;
				const dataset = e.currentTarget.dataset;
				this.$emit('click', {
					index: dataset.index
				});
			},
			handleClickCancel() {
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
	 "maskClosable" : 点击遮罩 是否可关闭,类型:"Boolean",默认值:true	
	 "show" :控制显示隐藏操作菜单,类型:"Boolean",默认值:false	
	 "itemList" :菜单按钮数组,类型:"Array",{text: 按钮显示文本,color: 按钮文本颜色},默认值:[{text: "确定",color: "#1a1a1a"}]
	 "tips":提示信息,类型:"String",默认值:""
	 "color":提示信息文字颜色,类型:"String",默认值:"#9a9a9a"
	 "size":提示文字大小,类型:"Number",默认值:26 (upx)
	 "isCancel": 否需要取消按钮,类型:"Boolean",默认值:true
	 
 methods:
   "px":upx转换为px,现在支持动态绑定rpx,后续会去掉
   "handleClickMask":遮罩层点击事件
   "handleClickItem":菜单按钮点击事件
   "handleClickCancel":取消关闭操作菜单事件

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 
