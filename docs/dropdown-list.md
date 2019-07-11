# dropdown-list
dropdown-list 下拉列表

## 组件结构
``` html
<template>
	<view class="tui-selected-class tui-dropdown-list" :style="{height:selectHeight?px(selectHeight):'auto'}">
		<slot name="selectionbox"></slot>
		<view class="tui-dropdown-view" :class="[show?'tui-dropdownlist-show':'']" :style="{background:bgcolor,height:px(show?height:0),top:px(top)}">
			<slot name="dropdownbox"></slot>
		</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiDropdownList",
		props: {
			//控制显示
			show: {
				type: Boolean,
				default: false
			},
			//背景颜色
			bgcolor: {
				type: String,
				default: "none"
			},
			//top  rpx
			top: {
				type: Number,
				default: 0
			},
			//下拉框高度 upx
			height: {
				type: Number,
				default: 0
			},
			//选择框高度 单位upx
			selectHeight: {
				type: Number,
				default: 0
			}
		},
		methods: {
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
	 "show" : 控制显示,类型:"Boolean",默认值:false	
	 "bgcolor" :背景颜色， 类型:"String",默认值:"none"
	 "top" :下拉框top值,类型:"Number",默认值:0
	 "height":下拉框高度 upx，类型:"Number",默认值:0
	 "selectHeight":下拉框父容器高度 单位upx，类型:"Number",默认值:0
	 
 methods:
   "px":upx转px，目前已支持动态绑定rpx，后期会移除

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 