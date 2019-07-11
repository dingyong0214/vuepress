# sticky
sticky吸顶容器

## 组件结构
``` html
<template>
	<view class="tui-sticky-class">
		<!--sticky 容器-->
		<view :class="[isFixed === true ? 'tui-sticky-fixed' : '']">
			<slot name="header"></slot>
		</view>
		<!--sticky 容器-->
		<!--内容-->
		<slot name="content"></slot>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiSticky",
		props: {
			scrollTop: {
				type: Number
			}
		},
		watch: {
			scrollTop(newValue, oldValue) {
				this.updateStickyChange();
			}
		},
		// #ifdef H5
		mounted() {
			this.updateScrollChange();
		},
		// #endif
		onReady() {
			this.updateScrollChange();
		},
		data() {
			return {
				timer: null,
				top: 0,
				height: 0,
				isFixed: false
			};
		},
		methods: {
			updateStickyChange() {
				const top = this.top;
				const height = this.height;
				const scrollTop = this.scrollTop
				this.isFixed = (scrollTop >= top && scrollTop < top + height) ? true : false
			},
			updateScrollChange() {
				if (this.timer) {
					clearTimeout(this.timer)
					this.timer = null
				}
				this.timer = setTimeout(() => {
					const className = '.tui-sticky-class';
					const query = uni.createSelectorQuery().in(this);
					query.select(className).boundingClientRect((res) => {
						if (res) {
							this.top = res.top;
							this.height = res.height
						}
					}).exec()
				}, 0)
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
	 "scrollTop" : 滚动条距离顶部距离,类型:"Number"
	 
 methods:
   "updateStickyChange":scrollTop与元素top比较，判断元素是否吸顶
   "updateScrollChange"：获取元素的top值，以及height值
   

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 