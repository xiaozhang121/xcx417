<template>
	<view class="date">
		  <van-cell
				class='left'
		       :value="start.timeValue"
		       @click="showStart" />
		<van-popup :show="start.show" @close="StartClose"  position="bottom">
			  <van-datetime-picker
			    type="datetime"
			    :value="start.currentDate"
			    :min-date="start.minDate"
				:max-date="start.maxDate"
				@confirm = 'startConfirmFn'
				@cancel = 'cancel'
			  />
		</van-popup> 
		<view class="mid">
			-
		</view>
		<van-cell
				class='right'
		       :value="end.timeValue"
		       @click="showEnd" />
		<van-popup :show="end.show" @close="EndClose"  position="bottom">
			  <van-datetime-picker
			    type="datetime"
			    :value="end.currentDate"
			    :min-date="end.minDate"
				@confirm = 'endConfirmFn'
				@cancel = 'cancel'
			  />
		</van-popup> 
			<van-icon class='ico' name="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAABV0lEQVRIS92VwU3DQBBF3wASuSUlUEJKSCnmgJwjdGBXQDhh5ZLQgVMBSQWYDtwBuZELHrRrm9iyE9YRllDmYq12dv7O/3/HQs8hPdfn3AGmui4o9IgkbdDp6wy4QZgRSZlbSztO0VQDID/YVsDsRxJQflsEbQL4ukUYFrlhAfB6wAwbIpkwVf3Zz3hgLqYzG02AarISIySA6aQtUoQAZVnZDG1XTgCnefh/ANRu4dSIpyMGfABOHRhxDa+LitgpyiPCCHghkiW+Go2GZKyssLl+nQC8AmDNjoQB93adkTCX2Nozj9QCdgLI/T1BUJ5lY8vc6ZgrhnzyzlK2jXUngPyBlf4P+SLmkrfixoYir+L/6ntwpKjiZSeRTVLHDvYiZzxxQVITeUfMNQsreu8i70V3dtHajoAukTG2U/VXm9aHXReIMvfWWvbgLDql5JEz5/7L/AO6vgGdT7oZrHsq9wAAAABJRU5ErkJggg==" />
	</view>
</template>
<script>
	   //import uniEcCanvas from '../../../uni-ec-canvas/uni-ec-canvas.vue' 
	  // import WxCanvas from "../../../uni-ec-canvas/wx-canvas";
	  // import * as echarts from "../../../uni-ec-canvas/echarts";
	   //import echarts from './echarts.js'
	export default {
		components: {
			  
		},
		mounted() {
			
		},
		// watch:{
		// 	start(){
		// 			this.end.minDate = this.start.timeValue
		// 	},
		// 	immediate: true,
		// 	deep: true
		// },
		data(){
			return {
			// formatter(type, value) {
			//       if (type === 'year') {
			//         return `${value}年`;
			//       } else if (type === 'month') {
			//         return `${value}月`;
			//       }
			//       return value;
			//     },
			start: {
				show: false,
				timeValue: '请选择开始时间',
				currentDate: new Date().getTime(),
				minDate: new Date(2019,1,1).getTime(),
				maxDate:new Date().getTime()
			},
			end: {
				show: false,
				timeValue: '请选择结束时间',
				currentDate: new Date().getTime(),
				minDate: new Date(2019,1,1).getTime(),
			}
			}
		},
			methods: {
				showStart() {
				    this.start.show = true
				  },
				  showEnd() {
				      this.end.show = true
				    },
				  StartClose() {
				   this.start.show=false
				  },
				  EndClose() {
				   this.end.show=false
				  },
			sele(e){
				this.currentindex = e
			},
			startConfirmFn(e){
				this.start.timeValue = this.timeFormat(new Date(e.detail));
				this.start.show = false;
				this.end.minDate = new Date(e.detail).getTime()
				this.$emit('starttime',this.start.timeValue);
			},
			endConfirmFn(e){
				this.end.timeValue = this.timeFormat(new Date(e.detail));
				this.end.show = false;
				//console.log(this.end.timeValue)
				this.start.maxDate = new Date(e.detail).getTime();
				this.$emit('endtime',this.end.timeValue)
			},
			timeFormat(time) { 
				let year = time.getFullYear();        
				let month = time.getMonth() + 1;        
				let day = time.getDate();
				let hour = time.getHours();
				let minute = time.getMinutes();
				let second = time.getSeconds();
				return year + '-' + month + '-' + day+' '+hour+':'+minute 
				},
				cancel(){
					this.start.show = false;
					this.end.show = false;
				}
	}
	}
</script>

<style lang="less">
	.date {
		width: 100%;
		overflow: hidden;
		background-color: #FFFFFF;
		margin-top: 20rpx;
		.mid {
			float: left;
			position: relative;
			top: 18rpx;
			left: 0;
			color: #333;
		}
		.left {
			float: left;
			margin-left: 30rpx;
			.van-cell__value{
				color: #333!important;
			}
		}
		.right {
			float: left;
			
			.van-cell__value{
				color: #333!important;
			}
		}
	}
	.ico {
		position: relative;
		top: 25rpx;
		
		right: 0;
		.van-icon--image {
			width: 48rpx!important;
			height: 48rpx!important;
		}
	}

</style>
