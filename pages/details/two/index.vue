<template>
	<view class="">
		<view class="choose">
			<view class="choose-time" v-for="(item,index) in choose" @click="sele(item,index)" :class="currentindex===index?'select':''" :key='index'>
				{{item}}
			</view>
		</view>
		<view class="date" v-if="currentindex===4">
			  <van-cell
					class='left'
			       :value="start.timeValue"
			       @click="showStart" />
					   <van-popup :show="start.show" @close="StartClose"  position="bottom">
					   	  <van-datetime-picker
					   	    type="date"
					   	    :value="start.currentDate"
					   	    :min-date="start.minDate"
							:max-date = "start.maxDate"
					   		@confirm = 'startConfirmFn'
							@cancel='cancel'
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
					@confirm = 'endConfirmFn'
					@cancel = 'cancel'
				  />
			</van-popup> 
				<van-icon class='ico' name="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAABV0lEQVRIS92VwU3DQBBF3wASuSUlUEJKSCnmgJwjdGBXQDhh5ZLQgVMBSQWYDtwBuZELHrRrm9iyE9YRllDmYq12dv7O/3/HQs8hPdfn3AGmui4o9IgkbdDp6wy4QZgRSZlbSztO0VQDID/YVsDsRxJQflsEbQL4ukUYFrlhAfB6wAwbIpkwVf3Zz3hgLqYzG02AarISIySA6aQtUoQAZVnZDG1XTgCnefh/ANRu4dSIpyMGfABOHRhxDa+LitgpyiPCCHghkiW+Go2GZKyssLl+nQC8AmDNjoQB93adkTCX2Nozj9QCdgLI/T1BUJ5lY8vc6ZgrhnzyzlK2jXUngPyBlf4P+SLmkrfixoYir+L/6ntwpKjiZSeRTVLHDvYiZzxxQVITeUfMNQsreu8i70V3dtHajoAukTG2U/VXm9aHXReIMvfWWvbgLDql5JEz5/7L/AO6vgGdT7oZrHsq9wAAAABJRU5ErkJggg==" />
		</view>
		  <view class="eca" >
			
		  <!-- <uni-ec-canvas
		   v-if="start.show===false&&end.show===false"
		    class="uni-ec-canvas"
		    id="uni-ec-canvas"
		    ref="uni-ec-canvas"
		    canvas-id="uni-ec-canvas"
		    :ec="ec"
		  ></uni-ec-canvas> -->
		  <uni-ec-canvas 
		   v-if="start.show===false&&end.show===false"
		            class="uni-ec-canvas"
		            id="uni-ec-canvas"
		            ref="uni-ec-canvas"
		            canvas-id="uni-ec-canvas"
		            :ec="ec"
		         ></uni-ec-canvas>
		  </view>	   
	</view>
</template>

<script>
	 import uniEcCanvas from '../../../uni-ec-canvas/uni-ec-canvas.vue'
	 import {$http} from "../../common/util.js"
	export default {
		components: {
			 uniEcCanvas
		
		},
		props:["postid"],
		mounted() {
			this.gethis();
		},
		onLoad(){
		},
		data(){
			return {
				//timeData: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
			eaa:false,	
			ec: {
			  option:  {
	color:['#0068FF','#FFB917','#00C3A2'],
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
        // {
        //     show: true,
        //     realtime: true,
        //     start: 30,
        //     end: 70,
        //     xAxisIndex: [0, 1]
        // },
        // {
        //     type: 'inside',
        //     realtime: true,
        //     start: 30,
        //     end: 70,
        //     xAxisIndex: [0, 1]
        // }
    ],
    grid: [{
        left: 50,
        right: 50,
        height: '30%'
    }, {
        left: 50,
        right: 50,
        top: '55%',
        height: '30%'
    }],
    xAxis: [
        {
                   type: 'category',
                   boundaryGap: false,
                   axisLine: {onZero: true},
                   data: [],
				    axisLabel: {
				                   interval:0 
				               }
               },
               {
                   gridIndex: 1,
                   type: 'category',
                   boundaryGap: false,
                   axisLine: {onZero: true},
                   data: [],
                   position: 'top',
				    axisLabel: {
				                   interval:0 
				               }
               }
    ],
    yAxis: [
        {
                    name: '流量(m^3/s)',//上左
                    type: 'value',
                },
                {
                    gridIndex: 1,//下左
                    name: '压力(kPa)',
                    type: 'value',
                    inverse: true
                },
        		{
        		    name: '开启度(%)',//上右
        		    type: 'value',
					position:'right'
					//inverse: true
        		}
    ],
    series: [
         {
                    name: '流量',//上左
                    type: 'line',
                    symbolSize: 8,
                    hoverAnimation: false,
        			itemStyle : {
        				  normal : {
        				   lineStyle:{
        				   color:'#0068FF'//设置折线线条颜色
        				   }
        				   }
        			},
                    data: [
        					
                    ]
                },
        		{
        		     name: '开启度',//上右
        		     type: 'line',
					 yAxisIndex: 2,
        			step: 'middle',
        			 itemStyle : {
        			  normal : {
        			   lineStyle:{
        			   color:'#FFB917'//设置折线线条颜色
        			   }
        			   }
        		},
        		     data: []
        		},
                {
                    name: '压力',//下左
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
        					
                    ]
                }
    ]
}
			},	
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
			},
			choose: ['小时','天','月','年','其他'],
			currentindex:0,
			type:'0',//类型
			myChart:'',
			xarr:[],//x轴坐标
			openDegree:[],//开启度
			avgFlowValue:[],//流量
			avgPressureValue:[],//压力
			endTime:'',
			startTime:''
			
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
			sele(item,e){
				this.start.timeValue = '请选择开始时间'
				this.end.timeValue = '请选择结束时间'
				this.startTime = ''
				this.endTime = ''
				this.xarr.length=0
				this.openDegree.length=0
				this.avgFlowValue.length=0
				this.avgPressureValue.length=0
				this.currentindex = e;
				//console.log(item)
				//this.date = item;
				this.type = e;
				//this.$emit("getChild",item)
				this.gethis()
			},
			startConfirmFn(e){
				this.startTime = ''
				this.xarr.length=0
				this.openDegree.length=0
				this.avgFlowValue.length=0
				this.avgPressureValue.length=0//先清零
				this.start.timeValue = this.timeFormat(new Date(e.detail));
				this.start.show = false;
				this.end.minDate = new Date(e.detail).getTime();
				this.startTime = this.timeFormat(new Date(e.detail))
				if(this.endTime!=''){
					this.gethis() //如果后选择开始时间也可调用
				}
			},
			endConfirmFn(e){
				this.endTime = ''
				this.xarr.length=0
				this.openDegree.length=0
				this.avgFlowValue.length=0
				this.avgPressureValue.length=0 //清零
				this.start.maxDate = new Date(e.detail).getTime();
				//this.end.minDate = new Date(e.detail).getTime();
				this.end.timeValue = this.timeFormat(new Date(e.detail));
				this.end.show = false;
				this.endTime=this.timeFormat(new Date(e.detail))
				console.log(this.startTime)
				if(this.startTime==''){
					uni.showToast({
						title:'请选择开始时间',
						icon:'none'
					})
					return
				}
				 this.gethis()
			},
			timeFormat(time) { 
				let year = time.getFullYear();        
				let month = time.getMonth() + 1;        
				let day = time.getDate();        
				return year + '-' + month + '-' + day      
				},
				gethis(){
					var that = this
					//console.log(that.postid)
					if(that.type==2){
						that.type=3
						// console.log(1)
					}else if(that.type==3){
						that.type=4
						// console.log(2)
					}else if(that.type==4){
						that.type=''
					}
					$http({
						url: '/venus/mobilePhone/historyFlowPressure',
						data: {
							 stationId:that.postid,
							 dateType:that.type,
							 endTime:that.endTime,
							 startTime:that.startTime
						},
						success(res){
							 //that.ec.option.xAxis[0].data = [1,2,3,4,5];	
							 console.log(res)
							res.data.map((item,index)=>{
								that.xarr.push(item.dateInfo)
								that.openDegree.push(item.openDegree)
								that.avgFlowValue.push(item.avgFlowValue)
								that.avgPressureValue.push(item.avgPressureValue)
							})
							that.xarr = that.xarr.map((item,index)=>{
								return item.replace('2020-', '')
							});
							
							that.ec.option.xAxis[0].data = that.xarr;
							that.ec.option.xAxis[1].data = that.xarr
							that.ec.option.series[0].data = that.avgFlowValue;
							that.ec.option.series[1].data = that.openDegree;
							that.ec.option.series[2].data = that.avgPressureValue;	
							// console.log(that.ec.option.series[2].data = that.avgPressureValue)
							
						}
					})
				},
				cancel(){
					this.start.show = false;
					this.end.show = false;
				}
				
		
					}
			
	}
</script>

<style lang="less">
.eca {
		width: 100%;
		height: 1200rpx;
		//margin-top: 30rpx;
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
		margin-bottom: 30rpx;
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
