# tips
消息提示：包括顶部提示，居中提示，底部提示。可切换提示框背景颜色

## 组件结构
``` html
<template>
	<block v-if="position=='top'">
		<view class='tui-tips-class tui-toptips' :class="['tui-'+type,show?'tui-top-show':'']">{{msg}}</view>
	</block>
	<block v-else>
		<view class='tui-tips-class tui-toast' :class="[position=='center'?'tui-centertips':'tui-bottomtips',show?'tui-toast-show':'']">
			<view class="tui-tips-content" :class="['tui-'+type]">
				{{msg}}
			</view>
		</view>
	</block>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name:"tuiTips",
		props: {
			//top bottom center
			position: {
				type: String,
				default: "top"
			}
		},
		data() {
			return {
				timer: null,
				show: false,
				msg: "无法连接到服务器~",
				//translucent,primary,green,warning,danger
				type: "translucent"
			};
		},
		methods: {
			showTips: function(options) {
				const {
					type = 'translucent',
						duration = 2000
				} = options;
				clearTimeout(this.timer);
				this.show = true;
				this.duration = duration < 2000 ? 2000 : duration;
				this.type = type;
				this.msg = options.msg;
				this.timer = setTimeout(() => {
					this.show = false;
					clearTimeout(this.timer);
					this.timer = null;
				}, duration);
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
	 "position":提示消息位置（top bottom center）,类型："String"，默认值："top"
	 
 methods:
   "showTips":显示提示消息。 参数类型:"Object",参数信息：
			   {
				   type: "translucent",//translucent,primary,green,warning,danger ,消息样式类型
				   msg: "4S后关闭提示框", //提示信息
				   duration: 4000 //显示多久关闭
			   }

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 