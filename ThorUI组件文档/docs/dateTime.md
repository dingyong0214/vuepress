# dateTime
日期时间选择器:picker-view扩展，日期时间选择器。

## 组件结构
``` html
<template>
	<view class="tui-datetime-picker">
		<view class="tui-mask" :class="{ 'tui-mask-show': isShow }" @touchmove.stop.prevent="stop" catchtouchmove="stop" @tap="hide"></view>
		<view class="tui-header" :class="{ 'tui-show': isShow }">
			<view class="tui-picker-header" @touchmove.stop.prevent="stop" catchtouchmove="stop">
				<view class="tui-btn-picker" :style="{ color: cancelColor }" hover-class="tui-opacity" :hover-stay-time="150"
				 @click="hide">取消</view>
				<view class="tui-btn-picker" :style="{ color: color }" hover-class="tui-opacity" :hover-stay-time="150" @click="btnFix">确定</view>
			</view>
			<view class="tui-picker-body">
				<picker-view :value="value" @change="change" class="tui-picker-view">
					<picker-view-column v-if="!reset && type!=4">
						<view class="tui-column-item" v-for="(item,index) in years" :key="index">
							{{ item }}<text class="tui-text">年</text>
						</view>
					</picker-view-column>
					<picker-view-column v-if="!reset && type!=4">
						<view class="tui-column-item" v-for="(item,index) in months" :key="index">
							{{ formatNum(item)}}<text class="tui-text">月</text>
						</view>
					</picker-view-column>
					<picker-view-column v-if="!reset && (type==1 || type==2)">
						<view class="tui-column-item" v-for="(item,index) in days" :key="index">
							{{ formatNum(item) }}<text class="tui-text">日</text>
						</view>
					</picker-view-column>
					<picker-view-column v-if="!reset && (type==1 || type==4)">
						<view class="tui-column-item" v-for="(item,index) in hours" :key="index">
							{{ formatNum(item) }}<text class="tui-text">时</text>
						</view>
					</picker-view-column>
					<picker-view-column v-if="!reset && (type==1 || type==4)">
						<view class="tui-column-item" v-for="(item,index) in minutes" :key="index">
							{{ formatNum(item) }}<text class="tui-text">分</text>
						</view>
					</picker-view-column>
				</picker-view>
			</view>
		</view>
	</view>
</template>
``` 

## 组件脚本
``` js
<script>
	export default {
		name: "tuiDatetime",
		props: {
			//1-日期+时间（年月日+时分） 2-日期(年月日) 3-日期(年月) 4-时间（时分）
			type: {
				type: Number,
				default: 1
			},
			//年份区间
			startYear: {
				type: Number,
				default: 1980
			},
			//年份区间
			endYear: {
				type: Number,
				default: 2050
			},
			//"取消"字体颜色
			cancelColor: {
				type: String,
				default: "#888"
			},
			//"确定"字体颜色
			color: {
				type: String,
				default: "#5677fc"
			},
			//设置默认显示日期 2019-08-01 || 2019-08-01 17:01 || 2019/08/01 
			setDateTime: {
				type: String,
				default: ""
			}
		},
		data() {
			return {
				isShow: false,
				years: [],
				months: [],
				days: [],
				hours: [],
				minutes: [],
				year: 0,
				month: 0,
				day: 0,
				hour: 0,
				minute: 0,
				startDate: "",
				endDate: "",
				value: [0, 0, 0, 0, 0],
				reset: false
			};
		},
		mounted() {
			this.initData();
		},
		computed: {
			yearOrMonth() {
				return `${this.year}-${this.month}`
			},
			propsChange() {
				return `${this.setDateTime}-${this.type}-${this.startYear}-${this.endYear}`
			}
		},
		watch: {
			yearOrMonth() {
				this.setDays();
			},
			propsChange() {
				this.reset = true
				setTimeout(() => {
					this.initData()
				}, 10);
			}
		},
		methods: {
			stop() {},
			formatNum: function(num) {
				return num < 10 ? "0" + num : num + "";
			},
			generateArray: function(start, end) {
				return Array.from(new Array(end + 1).keys()).slice(start)
			},
			getIndex: function(arr, val) {
				let index = arr.indexOf(val);
				return ~index ? index : 0
			},
			//日期时间处理
			initSelectValue() {
				let fdate = this.setDateTime.replace(/\-/g, '/');
				fdate = fdate && fdate.indexOf("/") == -1 ? `2020/01/01 ${fdate}` : fdate
				let time = null;
				if (fdate)
					time = new Date(fdate);
				else
					time = new Date();
				this.year = time.getFullYear()
				this.month = time.getMonth() + 1;
				this.day = time.getDate();
				this.hour = time.getHours();
				this.minute = time.getMinutes();
			},
			initData() {
				this.initSelectValue()
				this.reset = false
				switch (this.type) {
					case 1:
						this.value = [0, 0, 0, 0, 0];
						this.setYears();
						this.setMonths();
						this.setDays();
						this.setHours();
						this.setMinutes();
						break;
					case 2:
						this.value = [0, 0, 0];
						this.setYears();
						this.setMonths();
						this.setDays();
						break;
					case 3:
						this.value = [0, 0];
						this.setYears();
						this.setMonths();
						break;
					case 4:
						this.value = [0, 0];
						this.setHours();
						this.setMinutes();
						break;
					default:
						break;
				}
			},
			setYears() {
				this.years = this.generateArray(this.startYear, this.endYear);
				setTimeout(()=> {
					this.$set(this.value, 0, this.getIndex(this.years, this.year));
				}, 8);
			},
			setMonths() {
				this.months = this.generateArray(1, 12);
				setTimeout(()=> {
					this.$set(this.value, 1, this.getIndex(this.months, this.month));
				}, 8);
			},
			setDays() {
				if (this.type == 3 || this.type == 4) return;
				let totalDays = new Date(this.year, this.month, 0).getDate();
				this.days = this.generateArray(1, totalDays);
				setTimeout(()=> {
					this.$set(this.value, 2, this.getIndex(this.days, this.day));
				}, 8);
			},
			setHours() {
				this.hours = this.generateArray(0, 23);
				setTimeout(()=> {
					this.$set(this.value, this.value.length - 2, this.getIndex(this.hours, this.hour));
				}, 8);
				
			},
			setMinutes() {
				this.minutes = this.generateArray(0, 59);
				setTimeout(()=> {
					this.$set(this.value, this.value.length - 1, this.getIndex(this.minutes, this.minute));
				}, 8);
			},
			show() {
				setTimeout(() => {
					this.isShow = true;
				}, 50);
			},
			hide() {
				this.isShow = false;
			},
			change(e) {
				this.value = e.detail.value;
				switch (this.type) {
					case 1:
						this.year = this.years[this.value[0]];
						this.month = this.months[this.value[1]];
						this.day = this.days[this.value[2]];
						this.hour = this.hours[this.value[3]];
						this.minute = this.minutes[this.value[4]];
						break;
					case 2:
						this.year = this.years[this.value[0]];
						this.month = this.months[this.value[1]];
						this.day = this.days[this.value[2]];
						break;
					case 3:
						this.year = this.years[this.value[0]];
						this.month = this.months[this.value[1]];
						break;
					case 4:
						this.hour = this.hours[this.value[0]];
						this.minute = this.minutes[this.value[1]];
						break;
					default:
						break;
				}
	
			},
			btnFix() {
				let result = {};
				let year = this.year;
				let month = this.formatNum(this.month || 0);
				let day = this.formatNum(this.day || 0);
				let hour = this.formatNum(this.hour || 0);
				let minute = this.formatNum(this.minute || 0);
				switch (this.type) {
					case 1:
						result = {
							year: year,
							month: month,
							day: day,
							hour: hour,
							minute: minute,
							result: `${year}-${month}-${day} ${hour}:${minute}`
						}
						break;
					case 2:
						result = {
							year: year,
							month: month,
							day: day,
							result: `${year}-${month}-${day}`
						}
						break;
					case 3:
						result = {
							year: year,
							month: month,
							result: `${year}-${month}`
						}
						break;
					case 4:
						result = {
							hour: hour,
							minute: minute,
							result: `${hour}:${minute}`
						}
						break;
					default:
						break;
				}
				this.$emit("confirm", result);
				this.hide();
			}
		}
	};
</script>
``` 

## 组件样式

``` css
... 此处省略n行
``` 

## 脚本说明

``` js
 props: 
	 "type" : 1-日期+时间（年月日+时分） 2-日期(年月日) 3-日期(年月) 4-时间（时分）,类型:"Number",默认值:1	
	 "startYear" :年份区间，起始年份,类型:"Number",默认值:1980	
	 "endYear" :年份区间，结束年份,类型:"Number",默认值：2050
	 "cancelColor":"取消"字体颜色,类型:"String",默认值:"#888"
	 "color":"确定"字体颜色,类型:"String",默认值:"#5677fc"
	 "setDateTime":设置默认显示日期 2019-08-01 || 2019-08-01 17:01 || 2019/08/01 ,类型:"String",默认值:""
	 
 methods:
   "generateArray":生成数组
   "getIndex":获取索引
   "initSelectValue":初始化日期时间处理
   "initData":初始化数据
   "setYears":设置年份
   "setMonths":设置月份
   "setDays":设置日期
   "setHours":设置小时
   "setMinutes":设置分钟
   "show":显示，打开选择器
   "hide":隐藏，关闭选择器
   "change":picker-view change事件，选择数据
   "btnFix":确定事件,传回选择的日期时间

```

## 示例

``` js
... 此处省略n行,下载源码查看
``` 

## 预览图

![](https://thorui.cn/img/V140/1.png)