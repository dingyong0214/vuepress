# scroll-top
回到顶部，nvue回到顶部查看源码中首页【nvue商品列表】

## 组件结构
``` html
<template>
	<view class="tui-scroll-top" :style="{bottom:bottom+'rpx',right:right+'rpx'}" v-show="visible && toggle" @tap.stop="goTop">
		<image class="tui-scroll-top-img" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADwAAAA8CAYAAAA6/NlyAAACKklEQVRoQ+3b61HDMAwAYGkC1AlgBEaADcoEtBNQNoAJKBNQJqAbsAIjlAkiJhBnruG4XBO/1TNVfjZx4k+yXJ+bIpzYgSfmBQP/94xbhocZJqJLADhrJPNfzPwx1dfJDBPRHBHfGsH+dFNEbph5O9ZnH3iDiLeNgV+ZeZEKPq0Muyjta3jeSJa3WTXcCDKqm/a1FBWuBi9WzzAR3QFAPye4mnvWjJsamIgIAN4R0S1kfg8RcQuFa2ZmDbgKeAzbAzXR1cE+rDa6KjgUq4muBo7FaqGrgCcmqCUivgwmrUOfVZvIioOnsMy8mc1m8hfcdR0S0eJAIKqgi4J9WAc9BN6v2VXQxcAh2CmwFroIOBTrA2ugs8Ex2BBwbXQWOBYbCq6JTganYGPAtdBJ4FRsLLgGOhqcg00Bl0ZHgXOxqeCS6GBwCWwOuBQ6CFwKmwsugQ4FrxDxabjod2vj2F2KsaVlzH1G1t73zLz23ScJLCLLFGyJDPegIVpEioLdfpSL3gUAbFKxJcH98AYA97PKDgBWIftiQRn2DZOY8yWGdMzzhtcaOCd6IW0tw12nOspUH1Z60goZUVbDKVHKaWM1bDWcM378bW3S8sco7wqrYavhvBHka2017ItQ7nmrYavh3DE03V69holoh4jnrlsi8snMbhdF7TgGeI2I7l0tB35k5gc1LcBx/vNARFcA4LagJl/mrhEI9QzXQMTc08Ax0WrxWstwi1mL6fM3Q1/xTKsOmbgAAAAASUVORK5CYII="></image>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiScrollTop",
		props: {
			//回顶部按钮距离底部距离 rpx
			bottom: {
				type: Number,
				default: 120
			},
			//回顶部按钮距离右侧距离 rpx
			right: {
				type: Number,
				default: 24
			},
			//距离顶部多少距离显示 px
			top: {
				type: Number,
				default: 100
			},
			//滚动距离
			scrollTop: {
				type: Number
			}
		},
		watch: {
			scrollTop(newValue, oldValue) {
				this.change();
			}
		},
		data() {
			return {
				//判断是否显示
				visible: false,
				//控制显示，主要解决调用api滚到顶部fixed元素抖动的问题
				toggle: true
			};
		},
		methods: {
			goTop: function() {
				this.toggle = false;
				uni.pageScrollTo({
					scrollTop: 0,
					duration: 120
				})
				setTimeout(() => {
					this.toggle = true
				}, 220)
			},
			change() {
				let show = this.scrollTop > this.top;
				if ((show && this.visible) || (!show && !this.visible)) {
					return
				}
				this.visible = show
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
	 "bottom" : 回顶部按钮距离底部距离 rpx
	 "right":回顶部按钮距离右侧距离 rpx
	 "top":距离顶部多少距离显示 px
	 "scrollTop":滚动距离
	 
 methods:
   "goTop":返回顶部事件
   "change":当滚距离发生改变时执行，判断是否显示回顶部按钮

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 