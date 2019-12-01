# upload
upload 图片上传，需要根据上传接口实际返回数据进行调整。

## 组件结构
``` html
<template>
	<view class="tui-container">
		<view class="tui-upload-box">
			<view class="tui-image-item" v-for="(item,index) in imageList" :key="index">
				<image :src="item" class="tui-item-img" @tap.stop="previewImage(index)" mode="aspectFill"></image>
				<view v-if="!forbidDel" class="tui-img-del" @tap.stop="delImage(index)"></view>
				<view v-if="statusArr[index]!=1" class="tui-upload-mask">
					<view class="tui-upload-loading" v-if="statusArr[index]==2"></view>
					<text class="tui-tips">{{statusArr[index]==2?'上传中...':'上传失败'}}</text>
					<view class="tui-mask-btn" v-if="statusArr[index]==3" @tap.stop="reUpLoad(index)" hover-class="tui-hover"
					 :hover-stay-time="150">重新上传</view>
				</view>
			</view>
			<view v-if="isShowAdd" class="tui-upload-add" @tap="chooseImage">
				<view class="tui-upload-icon tui-icon-plus"></view>
			</view>
		</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: 'tuiUpload',
		props: {
			//初始化图片路径
			value: {
				type: Array,
				default () {
					return []
				}
			},
			//禁用删除
			forbidDel: {
				type: Boolean,
				default: false
			},
			//禁用添加
			forbidAdd: {
				type: Boolean,
				default: false
			},
			//服务器地址
			serverUrl: {
				type: String,
				default: ""
			},
			//限制数
			limit: {
				type: Number,
				default: 9
			},
			//项目名，默认为 file
			fileKeyName: {
				type: String,
				default: "file"
			}
		},
		data() {
			return {
				//图片地址
				imageList: [],
				//上传状态：1-上传成功 2-上传中 3-上传失败
				statusArr: []
			}
		},
		created() {
			this.imageList = [...this.value];
			for (let item of this.imageList) {
				this.statusArr.push("1")
			}
		},
		computed: {
			isShowAdd() {
				let isShow = true;
				if (this.forbidAdd || (this.limit && this.imageList.length >= this.limit)) {
					isShow = false;
				}
				return isShow
			}
		},
		methods: {
			// 重新上传
			reUpLoad(index) {
				this.$set(this.statusArr, index, "2")
				this.change()
				this.uploadImage(index, this.imageList[index]).then(() => {
					this.change()
				}).catch(() => {
					this.change()
				})
			},
			change() {
				let status = ~this.statusArr.indexOf("2") ? 2 : 1
				if (status != 2 && ~this.statusArr.indexOf("3")) {
					// 上传失败
					status = 3
				}
				this.$emit('complete', {
					status: status,
					imgArr: this.imageList
				})
			},
			chooseImage: function() {
				let _this = this;
				uni.chooseImage({
					count: _this.limit - _this.imageList.length,
					success: function(e) {
						let imageArr = [];
						for (let i = 0; i < e.tempFilePaths.length; i++) {
							let len = _this.imageList.length;
							if (len >= _this.limit) {
								uni.showToast({
									title: `最多可上传${_this.limit}张图片`,
									icon: "none"
								});
								break;
							}
							let path = e.tempFilePaths[i]
							imageArr.push(path)
							_this.imageList.push(path)
							_this.statusArr.push("2")
						}
						_this.change()
	
						let start = _this.imageList.length - imageArr.length
						for (let j = 0; j < imageArr.length; j++) {
							let index = start + j
							//服务器地址
							if (_this.serverUrl) {
								_this.uploadImage(index, imageArr[j]).then(() => {
									_this.change()
								}).catch(() => {
									_this.change()
								})
							} else {
								//无服务器地址则直接返回成功
								_this.$set(_this.statusArr, index, "1")
								_this.change()
							}
						}
					}
				})
			},
			uploadImage: function(index, url) {
				let _this = this;
				return new Promise((resolve, reject) => {
					uni.uploadFile({
						url: this.serverUrl,
						name: this.fileKeyName,
						header: {
							//设置请求头
						},
						formData: {},
						filePath: url,
						success: function(res) {
							console.log(res)
							if (res.statusCode == 200) {
								//返回结果 此处需要按接口实际返回进行修改
								let d = JSON.parse(res.data.replace(/\ufeff/g, "") || "{}")
								//判断code，以实际接口规范判断
								if (d.code % 100 === 0) {
									// 上传成功 d.url 为上传后图片地址，以实际接口返回为准
									d.url && (_this.imageList[index] = d.url)
									_this.$set(_this.statusArr, index, d.url ? "1" : "3")
								} else {
									// 上传失败
									_this.$set(_this.statusArr, index, "3")
								}
								resolve(index)
							} else {
								_this.$set(_this.statusArr, index, "3")
								reject(index)
							}
						},
						fail: function(res) {
							_this.$set(_this.statusArr, index, "3")
							reject(index)
						}
					})
				})
	
			},
			delImage: function(index) {
				this.imageList.splice(index, 1)
				this.statusArr.splice(index, 1)
				this.$emit("remove", {
					index: index
				})
				this.change()
			},
			previewImage: function(index) {
				if (!this.imageList.length) return;
				uni.previewImage({
					current: this.imageList[index],
					loop: true,
					urls: this.imageList
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

|参数			|类型								|描述				|默认值			|
| :------------:| :------------:					| :------------:	| :------------:|
|value			|<font color=#e96900>Array</font>	|初始化图片路径		|**[]**		|
|forbidDel		|<font color=#e96900>Boolean</font>	|禁用删除			|**false**		|
|forbidAdd		|<font color=#e96900>Boolean</font>	|禁用添加			|**false**		|
|serverUrl		|<font color=#e96900>String</font>	|服务器地址			|**""**		|
|limit			|<font color=#e96900>Number</font>	|限制数				|**9**		|
|fileKeyName	|<font color=#e96900>String</font>	|项目名，默认为file	|**file**		|

###  methods

|名称				|描述										|
|:------------:		|:------------:								|
|**reUpLoad**		|重新上传事件									|
|**change**			|上传、删除等操作结束后，返回状态和图片列表	|
|**chooseImage**	|选择图片									|
|**uploadImage**	|上传图片									|
|**delImage**		|删除图片									|
|**previewImage**	|预览图片									|

## 示例

``` js
... 此处省略n行,下载源码查看
``` 

## 预览图
## 
![](https://thorui.cn/img/V140/7.png)