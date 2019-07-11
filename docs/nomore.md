# nomore
nomore 没有更多了

## 组件结构
``` html
<template>
	<view class="tui-nomore-class tui-loadmore-none" v-if="visible">
		<view :class="[isDot?'tui-nomore-dot':'tui-nomore']">
			<view :style="{background:bgcolor}" :class="[isDot?'tui-dot-text':'tui-nomore-text']">{{isDot?dotText:text}}</view>
		</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiNomore",
		props: {
			//是否可见
			visible: {
				type: Boolean,
				default: false
			},
			//当前页面背景颜色
			bgcolor: {
				type: String,
				default: "#fafafa"
			},
			//是否以圆点代替 "没有更多了"
			isDot: {
				type: Boolean,
				default: false
			},
			//isDot为false时生效
			text: {
				type: String,
				default: "没有更多了"
			}
		},
		data() {
			return {
				dotText: "●"
			};
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
	 "visible" : 是否可见,类型:"Boolean",默认值:false
	 "bgcolor" : 当前页面背景颜色,类型:"String",默认值:"#fafafa"
	 "isDot" : 是否以圆点代替 "没有更多了",类型:"Boolean",默认值:false
	 "text" : 显示文本，isDot为false时生效,类型:"String",默认值:"没有更多了"
	 
 methods:
   无

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 