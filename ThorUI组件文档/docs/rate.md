# rate
Rate评分:可设置星星数，可设置大小颜色，支持手势touch选择

## 组件结构
``` html
<template>
	<view class="tui-rate-class tui-rate-box" @touchmove="touchMove">
		<block v-for="(item,index) in quantity" :key="index">
			<view class="tui-icon tui-relative" :class="['tui-icon-collection'+(hollow && (current<=index || (disabled && current<=index+1))?'':'-fill')]"
			 :data-index="index" @tap="handleTap" :style="{fontSize:size+'px',color:(current>index+1 || (!disabled && current>index))?active:normal}">
				<view class="tui-icon tui-icon-main tui-icon-collection-fill" v-if="disabled && current==index+1" :style="{fontSize:size+'px',color:active,width:percent+'%'}"></view>
			</view>
		</block>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiRate",
		props: {
			//数量
			quantity: {
				type: Number,
				default: 5
			},
			//当前选中
			current: {
				type: Number,
				default: 0
			},
			//当前选中星星分数(大于0，小于等于1的数)
			score: {
				type: [Number, String],
				default: 1
			},
			//禁用点击
			disabled: {
				type: Boolean,
				default: false
			},
			//大小
			size: {
				type: Number,
				default: 20
			},
			//未选中颜色
			normal: {
				type: String,
				default: "#b2b2b2"
			},
			//选中颜色
			active: {
				type: String,
				default: "#e41f19"
			},
			//未选中是否为空心
			hollow: {
				type: Boolean,
				default: false
			}
		},
		data() {
			return {
				pageX: 0,
				percent: 0
			};
		},
		created() {
			this.percent = Number(this.score || 0) * 100
		},
		watch: {
			score(newVal, oldVal) {
				this.percent = Number(newVal || 0) * 100
			}
		},
		methods: {
			handleTap(e) {
				if (this.disabled) {
					return;
				}
				const index = e.currentTarget.dataset.index;
				this.$emit('change', {
					index: Number(index) + 1
				})
			},
			touchMove(e) {
				if (this.disabled) {
					return;
				}
				if (!e.changedTouches[0]) {
					return;
				}
				const movePageX = e.changedTouches[0].pageX;
				const distance = movePageX - this.pageX;
	
				if (distance <= 0) {
					return;
				}
				let index = Math.ceil(distance / this.size);
				index = index > this.count ? this.count : index;
				this.$emit('change', {
					index: index
				})
			}
		},
		// #ifdef H5
		mounted() {
			const className = '.tui-rate-box';
			let query = uni.createSelectorQuery().in(this)
			query.select(className).boundingClientRect((res) => {
				this.pageX = res.left || 0
			}).exec()
		},
	
		// #endif
		onReady() {
			const className = '.tui-rate-box';
			let query = uni.createSelectorQuery().in(this)
			query.select(className).boundingClientRect((res) => {
				this.pageX = res.left || 0
			}).exec()
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
	 "quantity" : 数量,类型:"Number",默认值:5
	 "current" :  当前选中星星,类型:"Number",默认值:0
	 "score" :    当前选中星星分数(大于0，小于等于1的数),类型:"[Number, String]",默认值:1
	 "disabled" : 是否禁用点击,类型:"Boolean",默认值:false
	 "size" : 	  星星大小,类型:"Number",默认值:20
	 "normal" :   未选中颜色,类型:"String",默认值:"#b2b2b2"
	 "active" :   选中颜色,类型:"String",默认值:"#e41f19"
	 "hollow" :   未选中是否为空心,类型:"Boolean",默认值:false
	 
 methods:
   "handleTap":点击事件
   "touchMove":touch事件

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 