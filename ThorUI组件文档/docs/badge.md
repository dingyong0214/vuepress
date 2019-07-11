# badge
Badge 徽章

## 组件结构
``` html
<template>
	<view class="tui-badge-class" :class="[dot?'tui-badge-dot':'tui-badge','tui-'+type, size?'tui-badge-small':'']" v-if="visible">
		<slot></slot>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiBadge",
		props: {
			//primary,warning,green,danger,white，black，gray
			type: {
				type: String,
				default: 'primary',
			},
			// '', small
			size: {
				type: String,
				default: '',
			},
			//是否是圆点
			dot: {
				type: Boolean,
				default: false
			},
			//是否可见
			visible: {
				type: Boolean,
				default: true
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
	 "type" : 样式类型,可传入[primary,warning,green,danger,white，black，gray],类型:"String",默认值:"primary"	
	 "size" :大小设置, 可传入['', small]， 类型:"String",默认值:''	
	 "dot" :是否是圆点，不显内容,类型:"Boolean",默认值:false
	 "visible":是否可见，建议直接在页面上进行控制,类型:"Boolean",默认值:true
	 
 methods:
   无

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 