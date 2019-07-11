# grid-item
grid-item 宫格item，结合grid使用

## 组件结构
``` html
<template>
	<view class="tui-grid-class tui-grid" :class="[bottom?'':'tui-grid-bottom','tui-grid-'+(cell<2?3:cell)]" :hover-class="hover?'tui-item-hover':''"
	 :hover-stay-time="150" :style="{background:bgcolor}" @tap="handleClick">
		<view class='tui-grid-bg'>
			<slot></slot>
		</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiGridItem",
		props: {
			cell: {
				type: Number,
				default: 3
			},
			bgcolor: {
				type: String,
				default: "#fff"
			},
			//是否有点击效果
			hover: {
				type: Boolean,
				default: true
			},
			//底部线条
			bottom: {
				type: Boolean,
				default: true
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
	 "cell" : 多少列，可出入[2,3,4,5],类型:"Number",默认值:3
	 "bgcolor" : 背景颜色,类型:"String",默认值:"#fff"
	 "hover" : 是否有点击效果,类型:"Boolean",默认值:true
	 "bottom" : 底部线条是否需要,类型:"Boolean",默认值:true
	 "index" : grid-item索引,类型:"Number",默认值:0
	 
 methods:
   "handleClick":点击事件

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 