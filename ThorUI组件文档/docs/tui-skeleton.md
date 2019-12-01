# tui-skeleton
tui-skeleton 骨架屏，数据请求时常见到锁屏的loading动画，而现在越来越多的产品倾向于使用Skeleton Screen替代 。

## 组件结构
``` html
<view class="tui-skeleton-cmomon tui-skeleton-box" :style="{width: winWidth+'px', height:winHeight+'px', backgroundColor:backgroundColor}">
	<view class="tui-skeleton-cmomon" v-for="(item,index) in skeletonElements" :key="index" :style="{width: item.width+'px', height:item.height+'px', left: item.left+'px', top: item.top+'px',backgroundColor: skeletonBgColor,borderRadius:getRadius(item.skeletonType,borderRadius)}"></view>
	<view class="tui-loading" :class="[getLoadingType(loadingType)]" v-if="isLoading"></view>
</view>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiSkeleton",
		props: {
			//选择器(外层容器)
			selector: {
				type: String,
				default: "tui-skeleton"
			},
			//外层容器背景颜色
			backgroundColor: {
				type: String,
				default: "#fff"
			},
			//骨架元素背景颜色
			skeletonBgColor: {
				type: String,
				default: "#e9e9e9"
			},
			//骨架元素类型：矩形，圆形，带圆角矩形["rect","circular","fillet"]
			//默认所有，根据页面情况进行传值
			//页面对应元素class为：tui-skeleton-rect，tui-skeleton-circular，tui-skeleton-fillet
			//如果传入的值不在下列数组中，则为自定义class值，默认按矩形渲染
			skeletonType: {
				type: Array,
				default () {
					return ["rect", "circular", "fillet"]
				}
			},
			//圆角值，skeletonType=fillet时生效
			borderRadius: {
				type: String,
				default: "16rpx"
			},
			//骨架屏预生成数据：提前生成好的数据，当传入该属性值时，则不会再次查找子节点信息
			preloadData: {
				type: Array,
				default () {
					return []
				}
			},
			//是否需要loading
			isLoading: {
				type: Boolean,
				default: true
			},
			//loading类型[1-10]
			loadingType: {
				type: Number,
				default: 1
			}
		},
		created() {
			const res = uni.getSystemInfoSync();
			this.winWidth = res.windowWidth;
			this.winHeight = res.windowHeight;
			//如果有预生成数据，则直接使用
			this.isPreload(true)
		},
		// #ifdef H5
		mounted() {
			this.$nextTick(() => {
				this.nodesRef(`.${this.selector}`).then((res) => {
					this.winHeight = res[0].height + Math.abs(res[0].top)
				});
				!this.isPreload() && this.selectorQuery()
			})
	
		},
		// #endif
		onReady() {
			this.nodesRef(`.${this.selector}`).then((res) => {
				this.winHeight = res[0].height + Math.abs(res[0].top)
			});
			!this.isPreload() && this.selectorQuery()
		},
		data() {
			return {
				winWidth: 375,
				winHeight: 800,
				skeletonElements: []
			};
		},
		methods: {
			getLoadingType: function(type) {
				let value = 1
				if (type && type > 0 && type < 11) {
					value = type
				}
				return 'tui-loading-' + value
			},
			getRadius: function(type, val) {
				let radius = "0"
				if (type == "circular") {
					radius = "50%"
				} else if (type == "fillet") {
					radius = val
				}
				return radius;
			},
			isPreload(init) {
				let preloadData = this.preloadData || []
				if (preloadData.length) {
					init && (this.skeletonElements = preloadData)
					return true
				}
				return false
			},
			async selectorQuery() {
				let skeletonType = this.skeletonType || []
				let nodes = []
				for (let item of skeletonType) {
					let className = `.${this.selector} >>> .${item}`
					// #ifdef H5
					className = `.${item}`
					// #endif
					if (~"rect_circular_fillet".indexOf(item)) {
						// #ifndef H5
						className = `.${this.selector} >>> .${this.selector}-${item}`
						// #endif
						// #ifdef H5
						className = `.${this.selector}-${item}`
						// #endif
					}
					await this.nodesRef(className).then((res) => {
						res.map(d => {
							d.skeletonType = item
						})
						nodes = nodes.concat(res)
					})
				}
				this.skeletonElements = nodes
			},
			async nodesRef(className) {
				return await new Promise((resolve, reject) => {
					uni.createSelectorQuery().selectAll(className).boundingClientRect((res) => {
						if (res) {
							resolve(res);
						} else {
							reject(res)
						}
					}).exec();
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

|参数			|类型								|描述									|默认值								|
| :------------:| :------------:					| :------------:						| :------------:					|
|selector		|<font color=#e96900>String</font>	|选择器(外层容器)						|**tui-skeleton**					|
|backgroundColor|<font color=#e96900>String</font>	|外层容器背景颜色						|**#fff**							|
|skeletonBgColor|<font color=#e96900>String</font>	|骨架元素背景颜色						|**#e9e9e9**						|
|skeletonType	|<font color=#e96900>Array</font>	|骨架元素类型：矩形，圆形，带圆角矩形	|**["rect", "circular", "fillet"]**	|
|borderRadius	|<font color=#e96900>String</font>	|圆角值，skeletonType=fillet时生效		|**16rpx**							|
|preloadData	|<font color=#e96900>Array</font>	|骨架屏预生成数据						|**[]**								|
|isLoading		|<font color=#e96900>Boolean</font>	|是否需要loading						|**true**							|
|loadingType	|<font color=#e96900>Number</font>	|loading类型[1-10]						|**1**								|
###  methods

|名称				|描述					|
|:------------:		|:------------:			|
|**getLoadingType**	|获取loading类型		|
|**getRadius**		|获取圆角值				|
|**isPreload**		|骨架屏是否有预生成数据	|
|**selectorQuery**	|查找骨架元素节点		|
|**nodesRef**		|查找骨架元素节点api执行|

## 示例

``` js
... 此处省略n行,下载源码查看
``` 

## 预览图
## 
![](https://thorui.cn/img/V141/2.jpg)