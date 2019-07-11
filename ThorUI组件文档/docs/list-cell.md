# list-cell
list-cell 列表cell，可结合list-view使用

## 组件结构
``` html
<template>
	<view class="tui-cell-class tui-list-cell" :class="{'tui-cell-arrow':arrow,'tui-cell-last':last}" :hover-class="hover?'tui-cell-hover':''"
	 :style="{background: bgcolor,fontSize: px(size),color:color}" :hover-stay-time="150" @tap="handleClick">
		<slot></slot>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiListCell",
		props: {
			arrow: {
				type: Boolean,
				default: false //是否有箭头
			},
			hover: {
				type: Boolean,
				default: true //是否有点击效果
			},
			last: {
				type: Boolean,
				default: false //最后一条数据隐藏线条
			},
			bgcolor: {
				type: String,
				default: "#fff" //背景颜色
			},
			size: {
				type: Number,
				default: 32 //字体大小
			},
			color: {
				type: String,
				default: "#333" //字体颜色
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
			px: function(num) {
				return uni.upx2px(num) + 'px';
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
	 "arrow" : 是否有箭头,类型:"Boolean",默认值:"false"
	 "hover" : 是否有点击效果，类型:"Boolean",默认值:true
	 "last" : 去掉数据线条，类型:"Boolean",默认值:false
	 "bgcolor" : 背景颜色，类型:"String",默认值:#fff
	 "size" : 字体大小，类型:"Number",默认值:32upx
	 "color" : 字体颜色，类型:"String",默认值:"#333"
	 "index" : list-cell索引，类型:"Number",默认值:0
	 
 methods:
   "handleClick":点击事件
   "px":upx转px，已经支持rpx，后续调整

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 