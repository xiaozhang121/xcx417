<template>
	<view class="">
		<view class="choose">
			<view class="choose-time" v-for="(item,index) in choose" @click="sele(index)" :class="currentindex===index?'select':''" :key='index'>
				{{item}}
			</view>
		</view>
		<view class="date">
			  <van-cell
					class='left'
			       :value="start.timeValue"
			       @click="showStart" />
			<van-popup :show="start.show" @close="StartClose"  position="bottom">
				  <van-datetime-picker
				    type="date"
				    :value="start.currentDate"
				    :min-date="start.minDate"
				    :formatter="formatter"
					@confirm = 'startConfirmFn'
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
				    type="date"
				    :value="end.currentDate"
				    :min-date="end.minDate"
				    :formatter="formatter"
					@confirm = 'endConfirmFn'
				  />
			</van-popup> 
				<van-icon class='ico' name="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAABV0lEQVRIS92VwU3DQBBF3wASuSUlUEJKSCnmgJwjdGBXQDhh5ZLQgVMBSQWYDtwBuZELHrRrm9iyE9YRllDmYq12dv7O/3/HQs8hPdfn3AGmui4o9IgkbdDp6wy4QZgRSZlbSztO0VQDID/YVsDsRxJQflsEbQL4ukUYFrlhAfB6wAwbIpkwVf3Zz3hgLqYzG02AarISIySA6aQtUoQAZVnZDG1XTgCnefh/ANRu4dSIpyMGfABOHRhxDa+LitgpyiPCCHghkiW+Go2GZKyssLl+nQC8AmDNjoQB93adkTCX2Nozj9QCdgLI/T1BUJ5lY8vc6ZgrhnzyzlK2jXUngPyBlf4P+SLmkrfixoYir+L/6ntwpKjiZSeRTVLHDvYiZzxxQVITeUfMNQsreu8i70V3dtHajoAukTG2U/VXm9aHXReIMvfWWvbgLDql5JEz5/7L/AO6vgGdT7oZrHsq9wAAAABJRU5ErkJggg==" />
		</view>
		
		  <view class="eca">
		  <uni-ec-canvas
		    class="uni-ec-canvas"
		    id="line-chart"
		    ref="canvas"
		    canvas-id="lazy-load-chart"
		    :ec="ec"
		  ></uni-ec-canvas>
		  </view>	   
	
	</view>
</template>

<script>
	 import uniEcCanvas from '../../../uni-ec-canvas/uni-ec-canvas.vue'
	 
	export default {
		components: {
			 uniEcCanvas
		
		},
		mounted() {
		},
		data(){
			return {
				timeData: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
			ec: {
			  option: {
    tooltip: {
        trigger: 'axis',
        axisPointer: {
            animation: false
        }
    },
    legend: {
        data: ['流量', '压力','开启度']
    },
    axisPointer: {
        link: {xAxisIndex: 'all'}
    },
    // dataZoom: [
    //         {
    //             show: true,
    //             realtime: true,
    //             start: 30,
    //             end: 70,
    //             xAxisIndex: [0, 1],
				// top: '30%'
    //         },
    //         {
    //             type: 'inside',
    //             realtime: true,
    //             start: 30,
    //             end: 70,
    //             xAxisIndex: [0, 1],
				// top: '30%'
    //         }
    //     ],
    grid: [{
        left: 40,
        right: 40,
        height: '15%'
    }, {
        left: 40,  
        right: 40,
        top: '30%',
        height: '15%'
    }],
    xAxis: [
        {
            type: 'category',
            boundaryGap: false,
            axisLine: {onZero: true},
            data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
        },
        {
            gridIndex: 1,
            type: 'category',
            boundaryGap: false,
            axisLine: {onZero: true},
            data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
            position: 'top'
        }
    ],
    yAxis: [
        {
            name: '流量(m^3/s)',
            type: 'value',
            max: 500
        },
        {
            gridIndex: 1,
            name: '降雨量(mm)',
            type: 'value',
			max: 8,
            inverse: true
        },
		{
		    // gridIndex: 1,
		    name: '开启度(%)',
		    type: 'value',
			max: 8,
			// axisLabel: {
			//    show: true,
			//       interval: 'auto',//居中显示
			//    formatter: '{value} %'//以百分比显示
			//                         },
		    //inverse: true
		}
    ],
    series: [
        {
            name: '流量',
            type: 'line',
            symbolSize: 8,
            hoverAnimation: false,
			itemStyle : {
				  normal : {
				   lineStyle:{
				   color:'#FFB917'//设置折线线条颜色
				   }
				   }
			},
            data: [
					0,1,1,1,1,2
            ]
        },
		{
		     name: '压力',
		     type: 'line',
			step: 'middle',
			 itemStyle : {
			  normal : {
			   lineStyle:{
			   color:'#0068FF'//设置折线线条颜色
			   }
			   }
		},
		     data: [220, 282, 201, 234, 290, 430, 410]
		},
        {
            name: '开启度',
            type: 'line',
            xAxisIndex: 1,
            yAxisIndex: 1,
            symbolSize: 8,
            hoverAnimation: false,
			itemStyle : {
				  normal : {
				   lineStyle:{
				   color:'#00C3A2'//设置折线线条颜色
				   }
				   }
			},
            data: [
					0,0,0,0,0,0,1
            ]
        }
    ]
}
			},	
			formatter(type, value) {
			      if (type === 'year') {
			        return `${value}年`;
			      } else if (type === 'month') {
			        return `${value}月`;
			      }
			      return value;
			    },
			start: {
				show: false,
				timeValue: '请选择开始时间',
				currentDate: new Date().getTime(),
				minDate: new Date().getTime(),
			},
			end: {
				show: false,
				timeValue: '请选择结束时间',
				currentDate: new Date().getTime(),
				minDate: new Date().getTime(),
			},
			choose: ['小时','天','月','年','其他'],
			currentindex:0,
			myChart:''
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
			},
			endConfirmFn(e){
				this.end.timeValue = this.timeFormat(new Date(e.detail));
				this.end.show = false;
			},
			timeFormat(time) { 
				let year = time.getFullYear();        
				let month = time.getMonth() + 1;        
				let day = time.getDate();        
				return year + '年' + month + '月' + day + '日'      
				}
					}
			
	}
</script>

<style lang="less">
.eca {
		width: 100%;
		height: 700px;
	}
	.uni-ec-canvas {
		width: 100%;
		height: auto;
		display: block;
		font-size: 12rpx;
	}
	
	.date {
		width: 100%;
		overflow: hidden;
		
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
	.uni-ec-canvas {
		width: 100%;
		height: 100%;
		display: block;
	}
	.choose {
		padding: 36rpx 48rpx;
		background-color: rgb(243, 243, 243);
		display: flex;
		.choose-time {
			font-size: 28rpx;
			height: 56rpx;
			background-color: #CCCCCC;
			flex: 1;
			text-align: center;
			margin-right: 20rpx;
			line-height: 56rpx;
			border-radius: 30rpx;
			color: #FFFFFF;
			}
			.select {
				background-color: #005AC3;
			}
			view:nth-child(5) {
					margin-right: 0;
		}
	}
</style>
