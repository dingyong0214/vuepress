# button
button 按钮,和基础组件button略有不同，支持设置任意大小

## 组件结构
``` html
<template>
	<button class="tui-btn-class tui-btn" :class="[plain?'tui-'+type+'-outline':'tui-btn-'+(type || 'primary'),getDisabledClass(disabled,type),getShapeClass(shape,plain),getShadowClass(type,shadow,plain)]"
	 :hover-class="getHoverClass(disabled,type,plain)" :style="{width:width,height:height,lineHeight:height,fontSize:size+'rpx'}"
	 :loading="loading" :disabled="disabled" @tap="handleClick">
		<slot></slot>
	</button>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiButton",
		props: {
			//样式类型 primary, white, danger, warning, green,blue, gray
			type: {
				type: String,
				default: 'primary'
			},
			//是否加阴影 type =primary和 danger有效
			shadow: {
				type: Boolean,
				default: false
			},
			// 宽度 rpx或 %
			width: {
				type: String,
				default: '100%'
			},
			//高度 rpx
			height: {
				type: String,
				default: '94rpx'
			},
			//字体大小 rpx
			size: {
				type: Number,
				default: 32
			},
			//形状 circle(圆角), square(默认方形)，rightAngle(平角)
			shape: {
				type: String,
				default: 'square'
			},
			plain: {
				type: Boolean,
				default: false
			},
			disabled: {
				type: Boolean,
				default: false
			},
			loading: {
				type: Boolean,
				default: false
			}
		},
		methods: {
			handleClick() {
				if (this.disabled) {
					return false;
				}
				this.$emit('click', {})
			},
			getShadowClass: function(type, shadow,plain) {
				let className = '';
				if (shadow && type != 'white' && !plain) {
					className = 'tui-shadow-' + type;
				}
				return className;
			},
			getDisabledClass: function(disabled, type) {
				let className = '';
				if (disabled && type != 'white' && type != 'gray') {
					className = 'tui-dark-disabled';
				}
				return className;
			},
			getShapeClass: function(shape, plain) {
				let className = '';
				if (shape == 'circle') {
					className = plain ? 'tui-outline-fillet' : 'tui-fillet';
				} else if (shape == "rightAngle") {
					className = plain ? 'tui-outline-rightAngle' : 'tui-rightAngle';
				}
				return className;
			},
			getHoverClass: function(disabled, type, plain) {
				let className = '';
				if (!disabled) {
					className = plain ? 'tui-outline-hover' : ('tui-' + (type || 'primary') + '-hover');
				}
				return className;
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
	 "type" : 样式类型，可传入[primary, white, danger, warning, green,blue, gray] 类型:"String",默认值:"primary"	
	 "shadow":否加阴影 ，默认false
	 "width":按钮宽度 rpx或 % ，默认100%
	 "height":按钮高度 rpx ，默认94rpx
	 "size" :按钮字体大小 rpx
	 "shape" :按钮形状，可传入[circle(圆角), square(默认方形)，rightAngle(平角)],类型:"String",默认值:"square"
	 "plain":是否空心,类型:"Boolean",默认值:false
	 "disabled":是否禁用,类型:"Boolean",默认值:false
	 "loading":是否显示加载图标,类型:"Boolean",默认值:false
	 
 methods:
   "handleClick":按钮点击事件
   "getShadowClass":获取阴影样式
   "getDisabledClass":禁用样式class获取
   "getShapeClass":按钮形状class获取
   "getHoverClass":点击效果 class获取

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 