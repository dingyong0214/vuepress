# tabs
tabs标签页，支持自定义设置，具体查看文档。暂不支持超出一屏，滚动标签页参考项目中的示例。

## 组件结构
``` html
<template>
	<view class="tui-tabs-view" :class="[isFixed?'tui-tabs-fixed':'tui-tabs-relative',unlined?'tui-unlined':'']" :style="{height:height+'rpx',padding:`0 ${padding}rpx`,background:bgColor,top:isFixed?top+'px':'auto'}">
		<view v-for="(item,index) in tabs" :key="index" class="tui-tabs-item" :style="{width:itemWidth}" @tap.stop="swichTabs(index)">
			<view class="tui-tabs-title" :class="{'tui-tabs-active':currentTab==index,'tui-tabs-disabled':item.disabled}" :style="{color:currentTab==index?selectedColor:color,fontSize:size+'rpx',lineHeight:size+'rpx',fontWeight:bold && currentTab==index?'bold':'normal'}">{{item.name}}</view>
		</view>
		<view class="tui-tabs-slider" :style="{transform:'translateX('+scrollLeft+'px)',width:sliderWidth+'rpx',height:
	sliderHeight+'rpx',bottom:bottom+'rpx',background:sliderBgColor}"></view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiTabs",
		props: {
			//标签页
			tabs: {
				type: Array,
				default () {
					return []
				}
			},
			//rpx
			height: {
				type: Number,
				default: 80
			},
			//rpx 只对左右padding起作用，上下为0
			padding: {
				type: Number,
				default: 30
			},
			//背景色
			bgColor: {
				type: String,
				default: "#FFFFFF"
			},
			//是否固定
			isFixed: {
				type: Boolean,
				default: false
			},
			//px
			top: {
				type: Number,
				// #ifndef H5
				default: 0
				// #endif
				// #ifdef H5
				default: 44
				// #endif
			},
			//是否去掉底部线条
			unlined: {
				type: Boolean,
				default: false
			},
			//当前选项卡
			currentTab: {
				type: Number,
				default: 0
			},
			//滑块宽度
			sliderWidth: {
				type: Number,
				default: 68
			},
			//滑块高度
			sliderHeight: {
				type: Number,
				default: 6
			},
			//滑块背景颜色
			sliderBgColor: {
				type: String,
				default: "#5677fc"
			},
			//滑块bottom
			bottom: {
				type: Number,
				default: 0
			},
			//标签页宽度
			itemWidth: {
				type: String,
				default: "25%"
			},
			//字体颜色
			color: {
				type: String,
				default: "#666"
			},
			//选中后字体颜色
			selectedColor: {
				type: String,
				default: "#5677fc"
			},
			//字体大小
			size: {
				type: Number,
				default: 28
			},
			//选中后 是否加粗 ，未选中则无效
			bold:{
				type: Boolean,
				default: false
			}
		},
		watch:{
			currentTab(){
				this.checkCor();
			}
		},
		created() {
			setTimeout(() => {
				// 高度自适应
				uni.getSystemInfo({
					success: (res) => {
						this.winWidth = res.windowWidth;
						this.checkCor()
					}
				});
			}, 50);
		},
		data() {
			return {
				winWidth: 0,
				scrollLeft: 0
			};
		},
		methods: {
			checkCor: function() {
				let tabsNum = this.tabs.length
				let padding = this.winWidth / 750 * this.padding
				let width = this.winWidth - padding * 2
				let left = (width / tabsNum - (this.winWidth / 750 * this.sliderWidth)) / 2 + padding
				let scrollLeft = left
				if (this.currentTab > 0) {
					scrollLeft = scrollLeft + (width / tabsNum) * this.currentTab
				}
				this.scrollLeft = scrollLeft
			},
			// 点击标题切换当前页时改变样式
			swichTabs: function(index) {
				let item = this.tabs[index]
				if (item && item.disabled) return;
				if (this.currentTab == index) {
					return false;
				} else {
					this.$emit("change", {
						index: Number(index)
					})
				}
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

|参数			|类型								|描述										|默认值								|
| :------------:| :------------:					| :------------:							| :------------:					|
|tabs			|<font color=#e96900>Array</font>	|标签页列表数据								|**[]**								|
|height			|<font color=#e96900>Number</font>	|高度，单位：rpx							|**80**								|
|padding		|<font color=#e96900>Number</font>	|只对左右padding起作用，上下为0，单位：rpx	|**30**								|
|bgColor		|<font color=#e96900>String</font>	|背景颜色									|**#FFFFFF**						|
|isFixed		|<font color=#e96900>Boolean</font>	|是否固定									|**false**							|
|top			|<font color=#e96900>Number</font>	|top值，isFixed为true时有效，单位：px		|app和小程序：**0**，H5为**44px**	|
|unlined		|<font color=#e96900>Boolean</font>	|是否去掉底部线条							|**false**							|
|currentTab		|<font color=#e96900>Number</font>	|当前选项卡									|**0**								|
|sliderWidth	|<font color=#e96900>Number</font>	|滑块宽度，单位：rpx						|**68**								|
|sliderHeight	|<font color=#e96900>Number</font>	|滑块高度，单位：rpx						|**6**								|
|sliderBgColor	|<font color=#e96900>String</font>	|滑块背景颜色								|**#5677fc**						|
|bottom			|<font color=#e96900>Number</font>	|滑块bottom值，单位：rpx					|**0**								|
|itemWidth		|<font color=#e96900>String</font>	|标签页宽度									|**25%**							|
|color			|<font color=#e96900>String</font>	|字体颜色									|**#666**							|
|selectedColor	|<font color=#e96900>String</font>	|选中后字体颜色								|**#5677fc**						|
|size			|<font color=#e96900>Number</font>	|字体大小									|**28**								|
|bold			|<font color=#e96900>Boolean</font>	|选中后 字体是否加粗 ，未选中则无效			|**false**							|

``` js
 props:
   "tabs 字段"：
		 "name": "全部", //标签页标题
		 "disabled": "false" //是否禁用点击
```

###  methods

|名称			|描述						|
|:------------:	|:------------:				|
|**checkCor**	|计算滑块需要滑动距离		|
|**swichTabs**	|点击标题切换到当前标签页	|

## 示例

``` js
... 此处省略n行,下载源码查看
``` 

## 预览图
![](https://thorui.cn/img/V140/5.png)