# button
button 按钮

## 组件结构
``` html
<template>
	<button class="tui-btn-class tui-btn" :class="['tui-btn-'+size,plain?'tui-'+type+'-outline':'tui-'+(type || 'gradual'),getDisabledClass(disabled,type),getShapeClass(shape,plain)]"
	 :hover-class="getHoverClass(disabled,type,plain)" :loading="loading" :disabled="disabled" :open-type="openType" @tap="handleClick"
	 @getuserinfo="bindgetuserinfo" :form-type="formType" v-if="!hidden">
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
			// primary, white, danger, warning, green, gray,gradual
			type: {
				type: String,
				default: 'gradual',
			},
			// block, mini, small
			size: {
				type: String,
				default: 'block',
			},
			// circle, square，rightAngle
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
				default: false,
			},
			loading: {
				type: Boolean,
				default: false,
			},
			openType: {
				type: String,
				default: ''
			},
			formType: {
				type: String,
				default: ''
			},
			hidden: {
				type: Boolean,
				default: false
			},
			bottom: {
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
			bindgetuserinfo({
				detail = {}
			} = {}) {
				this.$emit('getuserinfo', detail);
			},
			getDisabledClass: function(disabled, type) {
				var className = '';
				if (disabled && type != 'white' && type != 'gray') {
					className = type == 'gradual' ? 'btn-gradual-disabled' : 'tui-dark-disabled';
				}
				return className;
			},
			getShapeClass: function(shape, plain) {
				var className = '';
				if (shape == 'circle') {
					className = plain ? 'tui-outline-fillet' : 'tui-fillet';
				} else if (shape == "rightAngle") {
					className = plain ? 'tui-outline-rightAngle' : 'tui-rightAngle';
				}
				return className;
			},
			getHoverClass: function(disabled, type, plain) {
				var className = '';
				if (!disabled) {
					className = plain ? 'tui-outline-hover' : ('tui-' + (type || 'gradual') + '-hover');
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
	 "type" : 样式类型，可传入[primary, white, danger, warning, green, gray,gradual] 类型:"String",默认值:"gradual"	
	 "size" :按钮大小，可传入[block, mini, small] 类型:"String",默认值:"block"
	 "shape" :按钮形状，可传入[circle(圆角), square(默认方形)，rightAngle(平角)],类型:"String",默认值:"square"
	 "plain":是否空心,类型:"Boolean",默认值:false
	 "disabled":是否禁用,类型:"Boolean",默认值:false
	 "loading":是否显示加载图标,类型:"Boolean",默认值:false
	 "openType":开放能力，参考官方文档,类型:"String",默认值:""
	 "formType":用于 <form> 组件，参考官方文档,类型:"String",默认值:""
	 "hidden":是否移除，建议直接在页面控制,类型:"Boolean",默认值:false
	 
 methods:
   "handleClick":按钮点击事件
   "bindgetuserinfo":获取用户信息，参考官方文档
   "getDisabledClass":禁用样式class获取
   "getShapeClass":按钮形状class获取
   "getHoverClass":点击效果 class获取

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 