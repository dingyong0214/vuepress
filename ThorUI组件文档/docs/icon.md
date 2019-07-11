# icon
Icon 图标

## 组件结构
``` html
<template>
	<view class="tui-icon-class tui-icon" :class="'tui-icon-'+name" :style="{ color: color, fontSize: size + 'px' ,fontWeight:bold?'bold':'normal'}"
	  @tap="handleClick(index)" ></view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiIcon",
		props: {
			name: {
				type: String,
				default: ''
			},
			size: {
				type: Number,
				default: 32
			},
			color: {
				type: String,
				default: ''
			},
			bold: {
				type: Boolean,
				default: false
			},
			visible: {
				type: Boolean,
				default: true
			},
			index: {
				type: Number,
				default: 0
			}
		},
		methods:{
			handleClick(index) {
				this.$emit('click',{index}) 
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
	 "name" : 图标名称,类型:"String",默认值:"" 
	 "size" : 图标大小,类型:"Number",默认值:32px
	 "color" :图标颜色,类型:"String",默认值:""
	 "bold" : 是否加粗,类型:"Boolean",默认值:false
	 "visible" : 是否显示，建议直接在页面上控制,类型:"Boolean",默认值:true
	 "index" : 索引,类型:"Number",默认值:0
	 
 methods:
   "handleClick":点击事件

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 