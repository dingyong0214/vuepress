# Collapse
Collapse 折叠面板。

## 组件结构
``` html
<template>
	<view class="tui-collapse" :style="{backgroundColor:bgColor}">
		<view class="tui-collapse-head" :style="{backgroundColor:hdBgColor}" @tap.stop="handleClick">
			<view class="tui-header" :class="{'tui-opacity':disabled}">
				<slot name="title"></slot>
				<view class="tui-collapse-icon tui-icon-arrow" :class="{'tui-icon-active':isOpen}" :style="{color:arrowColor}" v-if="arrow"></view>
			</view>
		</view>
		<view class="tui-collapse-body" :style="{backgroundColor:bdBgColor,transform: isOpen ? 'translateY(0)' : `translateY(${translateY})`,height:isOpen?height:'0'}">
			<slot name="content"></slot>
		</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiCollapse",
		props: {
			//collapse背景颜色
			bgColor: {
				type: String,
				default: 'none'
			},
			//collapse-head 背景颜色
			hdBgColor: {
				type: String,
				default: '#fff'
			},
			//collapse-body 背景颜色
			bdBgColor: {
				type: String,
				default: 'none'
			},
			//collapse-body实际高度 open时使用
			height: {
				type: String,
				default: 'auto'
			},
			//close时translateY ，当bd高度固定时，建议值为0
			translateY: {
				type: String,
				default: '-50%'
			},
			//索引
			index: {
				type: Number,
				default: 0
			},
			//当前索引，index==current时展开
			current: {
				type: Number,
				default: -1
			},
			// 是否禁用
			disabled: {
				type: [Boolean, String],
				default: false
			},
			//是否带箭头
			arrow:{
				type: [Boolean, String],
				default: true
			},
			//箭头颜色
			arrowColor:{
				type: String,
				default: "#333"
			}
		},
		watch: {
			current() {
				this.updateCurrentChange()
			}
		},
		created() {
			this.updateCurrentChange()
		},
		data() {
			return {
				isOpen: false
			};
		},
		methods: {
			updateCurrentChange() {
				this.isOpen = this.index == this.current
			},
			handleClick() {
				if (this.disabled) return;
				this.$emit("click", {
					index: Number(this.index)
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

|参数			|类型											|描述											|默认值			|
| :------------:| :------------:								| :------------:								| :------------:|
|bgColor		|<font color=#e96900>String</font>				|collapse背景颜色								|**none**		|
|hdBgColor		|<font color=#e96900>String</font>				|collapse-head 背景颜色							|**#fff**		|
|bdBgColor		|<font color=#e96900>String</font>				|collapse-body 背景颜色							|**none**		|
|height			|<font color=#e96900>String</font>				|collapse-body实际高度 open时使用				|**auto**		|
|translateY		|<font color=#e96900>String</font>				|close时translateY ，当bd高度固定时，建议值为0	|**-50%**		|
|index			|<font color=#e96900>Number</font>				|当前折叠面板在列表中的索引						|**0**			|
|current		|<font color=#e96900>Number</font>				|当前索引，index==current时展开					|**-1**			|
|disabled		|<font color=#e96900>[Boolean, String]</font>	|是否禁用										|**false**		|
|arrow			|<font color=#e96900>[Boolean, String]</font>	|是否带箭头										|**true**		|
|arrowColor		|<font color=#e96900>String</font>				|箭头颜色										|**#333**		|


###  methods

|名称					|描述				|
|:------------:			|:------------:		|
|**updateCurrentChange**|更新折叠面板状态	|
|**handleClick**		|切换点击事件		|

## 示例

``` js
... 此处省略n行,下载源码查看
``` 

## 预览图
![](https://thorui.cn/img/V140/6.png)