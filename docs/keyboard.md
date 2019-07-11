# keyboard
keyboard 数字键盘，结合keyboard-input使用

## 组件结构
``` html
<template>
	<view>
		<view class="tui-keyboard-mask" :class="[show?'tui-mask-show':'']" v-if="mask" @tap="handleClose"></view>
		<view class="tui-keyboard" :class="[action?'tui-keyboard-action':'',show?'tui-keyboard-show':'']">
			<slot></slot>
			<view class="tui-keyboard-grids">
				<!--{{(index==9 || index==10 || index==11)?'tui-grid-bottom':''}}-->
				<view class="tui-keyboard-grid" :class="[(index==9 || index==11)?'tui-bg-gray':'']" v-for="(item,index) in itemList"
				 :key="index" hover-class="tui-keyboard-hover" :hover-stay-time="150" @tap="handleClick" :data-index="index">
					<view v-if="index<11" class="tui-keyboard-item" :class="[index==9?'tui-fontsize-32':'']">{{getKeyBoard(index,action)}}</view>
					<view v-else class="tui-keyboard-item">
						<view class="tui-icon tui-keyboard-delete"></view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name:"tuiKeyboard",
		props: {
			//是否需要mask
			mask: {
				type: Boolean,
				default: true
			},
			//控制键盘显示
			show: {
				type: Boolean,
				default: false
			},
			//是否直接显示，不需要动画，一般使用在锁屏密码
			action: {
				type: Boolean,
				default: true
			}
		},
		data() {
			return {
				itemList: [1,2,3,4,5,6,7,8,9,10,11,12]
			};
		},
		methods: {
			getKeyBoard: function(index, action) {
				var content = index + 1;
				if (index == 9) {
					content = action ? "取消" : "清除";
				} else if (index == 10) {
					content = 0;
				}
				return content;
			},
			//关闭
			handleClose() {
				if (!this.show) {
					return;
				}
				this.$emit('close', {});
			},
			handleClick(e) {
				if (!this.show) {
					return;
				}
				const dataset = e.currentTarget.dataset;
				this.$emit('click', {
					index: Number(dataset.index)
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
	 "mask" : 是否需要遮罩,类型:"Boolean",默认值:true
	 "show" : 控制键盘显示,类型:"Boolean",默认值:false
	 "action" :是否直接显示，不需要动画，一般使用在锁屏密码,类型:"Boolean",默认值:true
	 "bold" : 是否加粗,类型:"Boolean",默认值:false
	 "visible" : 是否显示，建议直接在页面上控制,类型:"Boolean",默认值:true
	 "index" : 索引,类型:"Number",默认值:0
	 
 methods:
   "getKeyBoard":获取按键文本
   "handleClose":关闭键盘
   "handleClick":键盘点击事件

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 