# bottom-popup
bottom-popup 底部弹出层

## 组件结构
``` html
<template>
	<view>
		<view class="tui-popup-class tui-bottom-popup" :class="{'tui-popup-show':show}" :style="{background:bgcolor,height:height?px(height):'auto'}">
			<slot></slot>
		</view>
		<view class="tui-popup-mask" :class="[show?'tui-mask-show':'']" v-if="mask" @tap="handleClose"></view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name:"tuiBottomPopup",
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
				default: "#fff"
			},
			//高度 upx
			height: {
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
			px(num){
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
	 "mask" : 是否需要mask， 类型:"Boolean",默认值:true	
	 "show" :控制显示， 类型:"Boolean",默认值:false
	 "bgcolor" :背景颜色,类型:"String",默认值:"#fff"
	 "height":高度 upx,类型:"Number",默认值:0(0表示auto)
	 
 methods:
   "handleClose":隐藏关闭bottom-popup
   "px":upx转换为px,现在支持动态绑定rpx,后续会去掉

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 