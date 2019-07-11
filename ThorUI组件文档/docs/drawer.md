# drawer
Drawer 抽屉

## 组件结构
``` html
<template>
	<view class="tui-drawer-class tui-drawer" :class="[visible ? 'tui-drawer-show' : '','tui-drawer-' + mode]">
		<view v-if="mask" class="tui-drawer-mask" @tap="handleMaskClick"></view>
		<view class="tui-drawer-container">
			<slot></slot>
		</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name:"tuiDrawer",
		props: {
			visible: {
				type: Boolean,
				default: false
			},
			mask: {
				type: Boolean,
				default: true
			},
			maskClosable: {
				type: Boolean,
				default: true
			},
			mode: {
				type: String,
				default: 'left' // left right
			}
		},
		methods: {
			handleMaskClick() {
				if (!this.maskClosable) {
					return;
				}
				this.$emit('close', {});
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
	 "visible" : 是否显示抽屉,类型:"Boolean",默认值:false	
	 "mask" :是否需要mask， 类型:"Boolean",默认值:true	
	 "maskClosable" :遮罩是否可点击,类型:"Boolean",默认值:true
	 "mode":左抽屉还是右抽屉，可传入[left right]，类型:"String",默认值:"left"
	 
 methods:
   "handleMaskClick":点击事件，关闭抽屉

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 