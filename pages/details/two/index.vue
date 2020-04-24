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
				   <cover-view>
					   <van-popup :show="start.show" @close="StartClose"  position="bottom">
					   	  <van-datetime-picker
					   	    type="date"
					   	    :value="start.currentDate"
					   	    :min-date="start.minDate"
					   	    :formatter="formatter"
					   		@confirm = 'startConfirmFn'
					   	  />
					   </van-popup> 
				   </cover-view>
			<view class="mid">
				-
			</view>
			<van-cell
					class='right'
			       :value="end.timeValue"
			       @click="showEnd" />
			<van-popup :show="end.show" @close="EndClose"  position="bottom">
				  <cover-view>
				<van-datetime-picker
				    type="date"
				    :value="end.currentDate"
				    :min-date="end.minDate"
				    :formatter="formatter"
					@confirm = 'endConfirmFn'
				  /></cover-view>
			</van-popup> 
				<van-icon class='ico' name="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAABV0lEQVRIS92VwU3DQBBF3wASuSUlUEJKSCnmgJwjdGBXQDhh5ZLQgVMBSQWYDtwBuZELHrRrm9iyE9YRllDmYq12dv7O/3/HQs8hPdfn3AGmui4o9IgkbdDp6wy4QZgRSZlbSztO0VQDID/YVsDsRxJQflsEbQL4ukUYFrlhAfB6wAwbIpkwVf3Zz3hgLqYzG02AarISIySA6aQtUoQAZVnZDG1XTgCnefh/ANRu4dSIpyMGfABOHRhxDa+LitgpyiPCCHghkiW+Go2GZKyssLl+nQC8AmDNjoQB93adkTCX2Nozj9QCdgLI/T1BUJ5lY8vc6ZgrhnzyzlK2jXUngPyBlf4P+SLmkrfixoYir+L/6ntwpKjiZSeRTVLHDvYiZzxxQVITeUfMNQsreu8i70V3dtHajoAukTG2U/VXm9aHXReIMvfWWvbgLDql5JEz5/7L/AO6vgGdT7oZrHsq9wAAAABJRU5ErkJggg==" />
		</view>
		  <view class="eca" v-if="start.show===false&&end.show===false">
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
			  option:  {
	color:['#0068FF','#00C3A2','#FFB917'],
    tooltip: {
        trigger: 'axis',
        axisPointer: {
            animation: false
        }
    },
    legend: {
        data:['流量', '压力','开启度']
    },
    axisPointer: {
        link: {xAxisIndex: 'all'}
    },
    dataZoom: [
        {
            show: true,
            realtime: true,
            start: 30,
            end: 70,
            xAxisIndex: [0, 1]
        },
        {
            type: 'inside',
            realtime: true,
            start: 30,
            end: 70,
            xAxisIndex: [0, 1]
        }
    ],
    grid: [{
        left: 50,
        right: 50,
        height: '35%'
    }, {
        left: 50,
        right: 50,
        top: '55%',
        height: '35%'
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
        		    name: '开启度(%)',
        		    type: 'value',
        			max: 8
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
		height: 1200rpx;
		margin-top: 30rpx;
		background-color: #FFFFFF;
		padding-top: 80rpx;
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
		background-color: #FFFFFF;
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
