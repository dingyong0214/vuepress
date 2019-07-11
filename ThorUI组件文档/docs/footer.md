# footer
Footer 页脚

## 组件结构
``` html
<template>
	<view class="tui-footer-class tui-footer" :class="[fixed?'tui-fixed':'']" :style='{background:bgcolor}'>
		<view class="tui-footer-link" v-if="navigate.length>0">
			<block v-for="(item,index) in navigate" :key="index">
				<navigator class="tui-link" hover-class="tui-link-hover" hover-stop-propagation="true" :style="{color:(item.color || '#596d96'),fontSize:px(item.size || 28)}"
				 :open-type="item.type" :url="item.url" :target="item.target" :delta="item.delta" :app-id="item.appid"
				 :path="item.path" :extra-data="item.extradata" :bindsuccess="item.bindsuccess" :bindfail="item.bindfail">{{item.text}}</navigator>
			</block>
		</view>
		<view class="tui-footer-copyright" :style="{color:color,fontSize:px(size)}">
			{{copyright}}
		</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiFooter",
		props: {
			//type target url delta appid path extradata bindsuccess bindfail text color size
			//链接设置  数据格式对应上面注释的属性值
			navigate: {
				type: Array,
				default: []
			},
			//底部文本
			copyright: {
				type: String,
				default: "All Rights Reserved."
			},
			//copyright 字体颜色
			color: {
				type: String,
				default: "#A7A7A7"
			},
			//copyright 字体大小
			size: {
				type: Number,
				default: 24
			},
			//footer背景颜色
			bgcolor: {
				type: String,
				default: "none"
			},
			//是否固定在底部
			fixed: {
				type: Boolean,
				default: true
			}
		},
		methods: {
			px(num) {
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
	 "navigate" : 链接设置,参考官方文档,类型:"Array",默认值:[]	
	 "copyright" :底部文本， 类型:"String",默认值:"All Rights Reserved."
	 "color" :copyright 字体颜色,类型:"String",默认值:"#A7A7A7"
	 "size":copyright 字体大小 upx，类型:"Number",默认值:24
	 "bgcolor":footer背景颜色，类型:"String",默认值:"none"
	 "fixed":是否固定在底部，类型:"Boolean",默认值:true
	 
 methods:
   "px":upx转px，目前已支持动态绑定upx，后期会移除

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 