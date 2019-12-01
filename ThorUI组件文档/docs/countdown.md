# countdown
countdown 倒计时：时分秒倒计时，支持设置大小，颜色等

## 组件结构
``` html
<template>
	<view class="tui-countdown-class tui-countdown-box">
		<view class="tui-countdown-item" :style="{background:bgcolor,borderColor:bcolor,minWidth:minwidth+'rpx',minHeight:minheight+'rpx'}"
		 v-if="hours">
			<view :class="[scale?'tui-countdown-scale':'']" :style="{fontSize:size+'rpx',color:color,lineHeight:size +'rpx'}">{{h}}</view>
		</view>
		<view class="tui-countdown-colon" :style="{lineHeight:colonsize+'rpx',fontSize:colonsize+'rpx',color:coloncolor}"
		 v-if="hours">:</view>
		<view class="tui-countdown-item" :style="{background:bgcolor,borderColor:bcolor,minWidth:minwidth+'rpx',minHeight:minheight+'rpx'}">
			<view :class="[scale?'tui-countdown-scale':'']" :style="{fontSize:size+'rpx',color:color,lineHeight:size +'rpx'}">{{i}}</view>
		</view>
		<view class="tui-countdown-colon" :style="{lineHeight:colonsize+'rpx',fontSize:colonsize+'rpx',color:coloncolor}">:</view>
		<view class="tui-countdown-item" :style="{background:bgcolor,borderColor:bcolor,minWidth:minwidth+'rpx',minHeight:minheight+'rpx'}">
			<view :class="[scale?'tui-countdown-scale':'']" :style="{fontSize:size+'rpx',color:color,lineHeight:size +'rpx'}">{{s}}</view>
		</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiCountdown",
		props: {
			//数字框最小宽度
			minwidth: {
				type: Number,
				default: 26
			},
			//数字框最小高度
			minheight: {
				type: Number,
				default: 26
			},
			//数字框border颜色
			bcolor: {
				type: String,
				default: "#333"
			},
			//数字框背景颜色
			bgcolor: {
				type: String,
				default: "#fff"
			},
			//数字框字体大小
			size: {
				type: Number,
				default: 24
			},
			//数字框字体颜色
			color: {
				type: String,
				default: "#333"
			},
			//是否缩放 0.8
			scale: {
				type: Boolean,
				default: false
			},
			//冒号大小
			colonsize: {
				type: Number,
				default: 28
			},
			//冒号颜色
			coloncolor: {
				type: String,
				default: "#333"
			},
			//剩余时间 
			time: {
				type: Object,
				default: {
						hours: 0,
						minute: 0,
						second: 0
					}
			},
			//是否包含小时
			hours: {
				type: Boolean,
				default: true
			}
		},
		data() {
			return {
				countdown: null,
				h: '00',
				i: '00',
				s: '00'
			};
		},
		created() {
			this.doLoop()
		},
		destroyed() {
			clearInterval(this.countdown)
			this.countdown = null
		},
		methods: {
			toSeconds(hours, minutes, seconds) {
				return (hours * 60 * 60) + (minutes * 60) + seconds
			},
			endOfTime() {
				clearInterval(this.countdown)
				this.countdown = null;
				this.$emit('end', {});
			},
			doLoop: function() {
				let seconds = this.toSeconds(this.time.hours || 0, this.time.minute || 0, this.time.second)
				this.countDown(seconds)
				this.countdown = setInterval(() => {
					seconds--
					if (seconds < 0) {
						this.endOfTime()
						return
					}
					this.countDown(seconds)
				}, 1000)
			},
			countDown(seconds) {
				let [hour, minute, second] = [0, 0, 0]
				if (seconds > 0) {
					hour = Math.floor(seconds / (60 * 60))
					minute = Math.floor(seconds / 60) - (hour * 60)
					second = Math.floor(seconds) - (hour * 60 * 60) - (minute * 60)
				} else {
					this.endOfTime()
				}
				hour = hour < 10 ? ('0' + hour) : hour
				minute = minute < 10 ? ('0' + minute) : minute
				second = second < 10 ? ('0' + second) : second
				this.h = hour;
				this.i = minute;
				this.s = second
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
	 "minwidth" : 数字框最小宽度,类型:"Number",默认值:26
	 "minheight" : 数字框最小高度,类型:"Number",默认值:26
	 "bcolor" : 数字框border颜色,类型:"String",默认值:"#333"
	 "bgcolor" : 数字框背景颜色,类型:"String",默认值:"#fff"
	 "size" : 数字框字体大小,类型:"Number",默认值:24
	 "color" : 数字框字体颜色,类型:"String",默认值:"#333"
	 "scale" : 是否缩放数字 0.8,类型:"Boolean",默认值:false
	 "colonsize" : 冒号大小,类型:"Number",默认值:28
	 "coloncolor" : 冒号颜色,类型:"String",默认值:"#333"
	 "time" : 剩余时间,类型:"Object",默认值:
			  {
				hours: 0,
				minute: 0,
				second: 0
			 }
	 "hours" : 是否包含小时,类型:"Boolean",默认值:true
	 
 methods:
   "toSeconds":将时间转化成秒
   "endOfTime":倒计时结束事件
   "doLoop":倒计时方法
   "countDown":倒计时时间显示处理

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 