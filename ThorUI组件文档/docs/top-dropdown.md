# top-dropdown
top-dropdown：顶部下拉弹层

## 组件结构
``` html
<template>
	<view>
		<view class="tui-top-dropdown tui-dropdown-box" :class="[show?'tui-dropdown-show':'']" :style="{height:height?px(height):'auto', background: bgcolor,paddingBottom: px(paddingbtm),transform: 'translateZ(0) translateY('+(show?px(translatey):'-100%')+')'}">
			<slot></slot>
		</view>
		<view class="tui-dropdown-mask" :class="[mask && show ?'tui-mask-show':'']" @tap="handleClose"></view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiTopDropdown",
		props: {
			//是否需要mask
			mask: {
				type: Boolean,
				default: true
			},
			//控制显示
			show: {
				type: Boolean,
				default: false
			},
			//背景颜色
			bgcolor: {
				type: String,
				default: "#f2f2f2"
			},
			//padding-bottom  upx
			paddingbtm: {
				type: Number,
				default: 0
			},
			//高度 upx
			height: {
				type: Number,
				default: 580
			},
			//移动距离 需要计算
			translatey: {
				type: Number,
				default: 0
			}
		},
		methods: {
			handleClose() {
				if (!this.show) {
					return;
				}
				this.$emit('close', {});
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
	 "mask":是否需要遮罩,类型："Boolean"，默认值：true
	 "show":控制显示,类型："Boolean"，默认值：false
	 "bgcolor":弹层背景颜色,类型："String"，默认值："#f2f2f2"
	 "paddingbtm":padding-bottom upx,类型："Number"，默认值：0
	 "height":高度 upx,类型："Number"，默认值：580
	 "translatey":移动距离,类型："Number"，默认值：0
	 
 methods:
   "handleClose":关闭弹层
   "px":upx转换为px，已经支持rpx，且支持动态绑定

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 