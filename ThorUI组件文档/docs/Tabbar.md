# Tabbar
Tabbar 类似uni-app原生tabbar组件，可用于自定义tabbar，自定义tabbar逻辑可参考小程序自定义tabbar，建议使用原生tabbar。
微信小程序使用案例：[https://github.com/dingyong0214/AfterSale](https://github.com/dingyong0214/AfterSale)

## 组件结构
``` html
<template>
	<view class="tui-tabbar" :class="{'tui-tabbar-fixed':isFixed,'tui-unlined':unlined}" :style="{background:backgroundColor}">
		<block v-for="(item,index) in tabBar" :key="index">
			<view class="tui-tabbar-item" :class="{'tui-item-hump':item.hump}"
			 :style="{backgroundColor:item.hump?backgroundColor:'none'}" @tap="tabbarSwitch(index,item.hump,item.pagePath,item.verify)">
				<view class="tui-icon-box" :class="{'tui-tabbar-hump':item.hump}">
					<image :src="current==index?item.selectedIconPath:item.iconPath" :class="[item.hump?'':'tui-tabbar-icon']"></image>
					<view :class="[item.isDot?'tui-badge-dot':'tui-badge']" :style="{color:badgeColor,backgroundColor:badgeBgColor}"
					 v-if="item.num">{{item.isDot?"":item.num}}</view>
				</view>
				<view class="tui-text-scale" :class="{'tui-text-hump':item.hump}" :style="{color:current==index?selectedColor:color}">{{item.text}}</view>
			</view>
		</block>
		<view :class="{'tui-hump-box':hump}" v-if="hump && !unlined"></view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiTabbar",
		props: {
			//当前索引
			current: {
				type: Number,
				default: 0
			},
			//字体颜色
			color: {
				type: String,
				default: "#666"
			},
			//字体选中颜色
			selectedColor: {
				type: String,
				default: "#5677FC"
			},
			//背景颜色
			backgroundColor: {
				type: String,
				default: "#FFFFFF"
			},
			//是否需要中间凸起按钮
			hump: {
				type: Boolean,
				default: false
			},
			//固定在底部
			isFixed: {
				type: Boolean,
				default: true
			},
			//tabbar
			// "pagePath": "/pages/my/my", 页面路径
			// "text": "thor", 标题
			// "iconPath": "thor_gray.png", 图标地址
			// "selectedIconPath": "thor_active.png", 选中图标地址
			// "hump": true, 是否为凸起图标
			// "num": 2,   角标数量
			// "isDot": true,  角标是否为圆点
			// "verify": true  是否验证  （如登录）
			tabBar: {
				type: Array,
				default () {
					return []
				}
			},
			//角标字体颜色
			badgeColor: {
				type: String,
				default: "#fff"
			},
			//角标背景颜色
			badgeBgColor: {
				type: String,
				default: "#F74D54"
			},
			unlined: {
				type: Boolean,
				default: false
			}
	
		},
		watch: {
			current() {
	           
			}
		},
		data() {
			return {
	
			};
		},
		methods: {
			tabbarSwitch(index, hump, pagePath,verify) {
				this.$emit("click", {
					index: index,
					hump: hump,
					pagePath: pagePath,
					verify:verify
				})
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

###   props

|参数			|类型								|描述					|默认值			|
| :------------:| :------------:					| :------------:		| :------------:|
|current		|<font color=#e96900>Number</font>	|当前tabbar索引			|**0**			|
|color			|<font color=#e96900>String</font>	|字体颜色				|**#666**		|
|selectedColor	|<font color=#e96900>String</font>	|字体选中颜色			|**#5677FC**	|
|backgroundColor|<font color=#e96900>String</font>	|背景颜色				|**#FFFFFF**	|
|hump			|<font color=#e96900>Boolean</font>	|是否需要中间凸起按钮	|**false**		|
|isFixed		|<font color=#e96900>Boolean</font>	|是否固定在底部			|**true**		|
|tabBar			|<font color=#e96900>Array</font>	|tabbar列表				|**[]**			|
|badgeColor		|<font color=#e96900>String</font>	|角标字体颜色			|**#fff**		|
|badgeBgColor	|<font color=#e96900>String</font>	|角标背景颜色			|**#F74D54**	|
|unlined		|<font color=#e96900>Boolean</font>	|去掉顶部细线			|**false**		|

``` js
 props:
   "tabBar 字段"：
		 "pagePath": "/pages/my/my", //页面路径
		 "text": "thor", //标题
		 "iconPath": "thor_gray.png", //图标地址
		 "selectedIconPath": "thor_active.png", //选中图标地址
		 "hump": true, //是否为凸起图标
		 "num": 2,   //角标数量
		 "isDot": true,  //角标是否为圆点
		 "verify": true  //是否验证  （如登录）
```

###  methods

|名称				|描述				|
|:------------:		|:------------:		|
|**tabbarSwitch**	|tababr切换点击事件	|

## 示例

``` js
... 此处省略n行,下载源码查看
``` 

## 预览图
![](https://thorui.cn/img/V140/4.png)