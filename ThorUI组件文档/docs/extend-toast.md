# toast
toast 提示

## 组件结构
``` html
 <template>
 	<view class="tui-toast" :class="[visible?'tui-toast-show':'',content?'tui-toast-padding':'',icon?'':'tui-unicon-padding']" :style="{width:getWidth(icon,content)}">
 		<image :src="imgUrl" class="tui-toast-img" v-if="icon"></image>
 		<view class="tui-toast-text" :class="[icon?'':'tui-unicon']">{{title}}</view>
 		<view class="tui-toast-text tui-content-ptop" v-if="content && icon">{{content}}</view>
 	</view>
 </template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiToast",
		props: {
		},
		data() {
			return {
				timer: null,
				//是否显示
				visible: false,
				//显示标题
				title: "操作成功",
				//显示内容
				content: "",
				//是否有icon
				icon:false,
				imgUrl:""
			};
		},
		methods: {
			show: function(options) {
				let {
					duration = 2000,
					icon=false
				} = options;
				clearTimeout(this.timer);
				this.visible = true;
				this.title = options.title || "";
				this.content = options.content || "";
				this.icon=icon;
				if(icon && options.imgUrl){
					this.imgUrl=options.imgUrl
				}
				this.timer = setTimeout(() => {
					this.visible = false;
					clearTimeout(this.timer);
					this.timer = null;
				}, duration);
			},
			getWidth(icon,content){
				let width="auto";
				if(icon){
					width=content?'420rpx':'360rpx'
				}
				return width
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
	 无  
	 
 data: 
	 "timer":定时器
	 "visible":是否显示,不需要传入
	 "title":显示标题
	 "content":显示内容
	 "icon":是否有icon
	 "imgUrl":icon图片地址
	 
 methods:
   "show":传入相应参数，调用显示toast
   "getWidth":根据内容获取toast宽度

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 