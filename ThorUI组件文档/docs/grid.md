# grid
Grid 宫格，结合grid-item使用

## 组件结构
``` html
<template>
	<view class="tui-grids" :class="{'tui-border-top':unlined}">
		<slot></slot>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name:"tuiGrid",
		props: {
			//是否去掉上线条
			unlined: {
				type: Boolean,
				default: false
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
	 "unlined" : 是否去掉上线条,类型:"Boolean",默认值:false
	 
 methods:
   无

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 