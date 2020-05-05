<template>
	<view class="box">
		
		<!-- 切换导航-导航 -->
		<van-nav-bar
			title="监测站点"
			fixed
		/>
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
			
			<map style="height: 92vh;width:100%;" :latitude="latitude" :longitude="longitude" :markers="marker" @markertap='mark' scale="5" @tap='show=false' >
				<view class="divide">
					<view class="left">
						<image src="../../static/imgage/basic/compass@2x.png" mode=""></image>
					</view>
					<view class="right">
						<view class="bad">
							<view class="img">
								<image src="../../static/imgage/basic/bad.png" mode=""></image>
							</view>
							<view class="tex">
								预警站点
							</view>
						</view>
						<view class="bad">
							<view class="img">
								<image src="../../static/imgage/basic/good.png" mode=""></image>
							</view>
							<view class="tex">
								正常站点
							</view>
						</view>
						<view class="bad">
							<view class="img">
								<image src="../../static/imgage/basic/now.png" mode=""></image>
							</view>
							<view class="tex">
								当前站点
							</view>
						</view>
					</view>
					
				</view>
			</map>
			
			<view class="bottom"  :class="show?'start':'end'">
				<view class="pull">
					<view class="squ">
					</view>
				</view>
				<view class="area">
					<van-icon name="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAABrklEQVRIS82UvTIDURTHfydFUhgzSjTkCSQNSSUaSyWegPRMqJQoVdbQ8waiskkjqoRG8gSiQZnKR2bkmisybHbv7s6YzDjl3bPnd/7nSxiyyZDj8w8Ad1djdDpFFHkg9a24gVAiHj8ivdAOqkKwgptyHsUpMGYI0kYoMGeVTBAzoBf8PFKPhFUTxB+gy/LeuQ/IfJDbJhFP+pXLH1B3tkAOfbJvfr/NeL+pbTJL9uC7AVBuAO4gSgpkF8++AtQq64jSvfltDTJWOipAuRwV12StnOut7pNExvIkbFIQDqiVqwjzLmhkQM1pITLl+jkmaWYXdengtpKiq+5CVYJhk+uODVL0aXJ/3vXSuU2xT9bai9aD2uU0EtNjGt1UN0l2uRUN8DUp5T2E3UgEQ/b63+BTUXdKICshkCYZq3+jPK7BgN5GVz078ROmSSKeCzp44edaQ946NsLaQFcvSCTW/3ZNdcTjgzyiikxO5Jgc7zEen+HxqYqSIzZ3jJc0vAfa4+RAT0ZvJ0ZH4KMLL699MQ9s7EwH9Si8RFoBbHm2Vp8PsP+uINKcmp3CFfx3wCdrRoMZxJibEgAAAABJRU5ErkJggg==" />
					<text>{{areamessage.stationName}}</text>
				</view>
				<view class="watch">
					<view class="mh">
						<view class="ec-text">
							<view class="text-bt">
								<text>流量</text>
								<br />
								<text>(m^3/h)</text>
							</view>
						</view>
						<view class="ech">
							<uni-ec-canvas
								v-if="show"
							   class="uni-ec-canvas"
							   id="uni-ec-canvas"
							   ref="uni-ec-canvas"
							   canvas-id="uni-ec-canvas"
							   :ec="ec"
							></uni-ec-canvas>
						</view>
					</view>
					<view class="kpa">
						<view class="ec-text">
							<view class="text-bt">
								<text>压力</text>
								<br />
								<text>(kPa)</text>
							</view>
						</view>
						<view class="ech">
							<uni-ec-canvas
							v-if="show"
							   class="uni-ec-canvas"
							   id="uni-ec-canvas"
							   ref="uni-ec-canvas"
							   canvas-id="uni-ec-canvas"
							   :ec="econe"
							></uni-ec-canvas>
						</view>
					</view>
				</view>
				<view class="local">
					<van-icon name='data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABQAAAAUCAYAAACNiR0NAAABPElEQVQ4T72UwVEDMQxFJTVAOoBUAOmAEkIFhMtqfaSChA64eXxaqIB0AB0QKiBUwHLNQWKc8TLGsdkNk4lvO5aev/SlRTjwwQPz4LhAa+0ZIs4RcQoAIwBoVXWpqnfGmHWuuqJCa+0lET0FUJrbisiVMeYlvcgCvTIiek1gHwBwGgE8dJIqzQKdcw8AcO2TVfVNVac+MbRgiYjnAfzIzLNYZQno+7NVg4iTqqpWXVJoxXN4bF3X9XgIULsgZv71aNM0o81m81m6LylsAeDEJ4nIjTHGt2B7rLUzImrC5xcze/d/Tm8Pw6gsiGglIheIuIjMGtbD4PJ73xaJyHiQy5nSdthpK7qAP1fPOefLm2eU3jLz/V6b0gXHM1mavV5T0pcj6I4Jg1YvV4ofl3h8SoYd9/fVNzb/MmVf6DcBtocVrvnaNQAAAABJRU5ErkJggg=='></van-icon>
					<text>地理位置: {{areamessage.address}}</text>
				</view>
				<view class="exercise">
					<view class="ex-left">
						<van-icon name='data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABQAAAAUCAYAAACNiR0NAAABP0lEQVQ4T92UwVHDQAxFVzr4SkqACnAHOBUwrgB8sewToQKGCkhO3vXFdBBTAdBBqABKcK57kBgxzoxJHJOEnLKn3Vnpjf6XRmCOfODIPHMCwKqqRt77V7UmCIJxkiTNkE2DksuyDJl5DgDnChGRL0SM0zRdbINuBRZFESHi3BgzWktumDnO8/ytD9oLLIriFhGrIWnMnOR5/rweswF0zmnQzSpQRF5EZKpvAJgAwHUHMiWi+y60D6imn7VB70QUOecmIiJZls2ccyr1qv1fEtEvS3olO+ekTXhkZm3Ej3xmHiNiZIx50DcRbeQPAkVkJiI1IurYLJk5bGXfHQQ0xjRBEFx0PfLef646v3eFLagmoljv1tq625RDgTrQ2l2156lb7c5Aa+0CAC6H5lBEPrIsC/+cw/+usxNYX/ta8A2QsYQVMYlVfgAAAABJRU5ErkJggg=='></van-icon>
						<text @click="enter(areamessage.id)">查看详情</text>
					</view>
					<view class="ex-right">
						<van-icon name='data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABQAAAAUCAYAAACNiR0NAAABCUlEQVQ4T+2TsW3DMBBF/7GQWmeCJBPEniDJCBlBjU7qPEKyQTqKlTJCNrC9gbKBsoFrFXcGDVMQDJmKEVVBCBDggXfv/n2QhJkXzczDHwFaa++IaGOMecnzvInZNDlyXdeLrus2AJaq2qZpusqybH8JGgUOYQNAkyTJ8yVoFFhVVUNEDyNqGmZejamcHNkXWWufjDF+7Ddmfv2Vh7MAT4oePUxEvgG0QaGI+PPtSeUXM38OFY+O7JxrAYSiHRGtVfUdgN9rAMdmAPbMfBMFDvzq81R1GwIiWgJYhFhEsrIsP/r7c4Odc744KJj86v5tFkVxHwPqJOUsgZl76370bK5p8A+8xq3x3AM+WFsVRHGfxgAAAABJRU5ErkJggg=='></van-icon>
						<text @click="report(areamessage.id)">数据上报</text>
					</view>
				</view>
			</view>
			
			
			
			
		</view>
	</view>
</template>

<script>
	import statusBar from "../../components/status-bar/index.vue"
	import WatchItem from "../../components/watch-item/index.vue"
	import uniEcCanvas from '../../uni-ec-canvas/uni-ec-canvas.vue'
	import {$http} from "../common/util.js"
	export default {
		name: "user",
		components: { 
			statusBar,
			WatchItem,
			 uniEcCanvas
		},
		data() {
			return{
				hei:'',
				goodico:'../../static/imgage/basic/good.png',
				badico:'../../static/imgage/basic/bad.png',
				eachico:'',
				nowico:'../../static/imgage/basic/now.png',
				tableData:[
					
				],//站点数据
				areamessage:{},//弹出框展示的站点信息
				show:false,//地图下标展示
				latitude: 32,  //纬度
				longitude: 118,  //经度
				marker:[
				],
				userId:'',
				stationNameOrCode:'',
				ec:{
			option:{
    series: [
        {
            name: '1',
            type: 'gauge',
            center: ['50%', 
			'55%'], // 默认全局居中
            radius: '100%',
            min: 0,
            max: 120,  
            splitNumber: 10,
            axisLine: { // 坐标轴线
                lineStyle: { // 属性lineStyle控制线条样式
                    color:  [
                    [1,new this.$echarts.graphic.LinearGradient(0, 0, 1, 0, [
                      {
                        offset: 0.1,
                        color: "#00C3A2"
                      },
                      {
                        offset: 0.6,
                        color: "#FFF700"
                      },
                      {
                        offset: 1,
                        color: "#FF2C00"
                      }
                    ])
                  ]
                ],
                    width: 5, //半径
                    shadowColor: '#fff', //默认透明
                    shadowBlur: 1,
					goodicon:'../../static/imgage/basic/good.png',//正常图标
					badicon:'../../static/imgage/basic/bad.png'//预警图标
                }
            },
            pointer: {
              width:3,
			  length: '60%'
            },
            axisLabel: {
                //show:false,
                // 坐标轴小标记
                textStyle: { // 属性lineStyle控制线条样式
                    fontWeight: 'bolder',
                    color: '#999999', //刻度数字颜色 隐藏
                    shadowColor: '#fff', //默认透明
                    shadowBlur: 10,
					fontSize: 5
                }
            },
            axisTick: { // 坐标轴小标记
                length: 5, // 属性length控制线长
                lineStyle: { // 属性lineStyle控制线条样式
                    color: '#999999', //坐标轴 小刻度线颜色
					width:1,
                },
				width:2
            },
            splitLine: { // 分隔线
                length: 5, // 属性length控制线长
                lineStyle: { // 属性lineStyle（详见lineStyle）控制线条样式
                    width: 3,
                    color: 'transparent', //分割线
                    shadowColor: '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            title: {
                textStyle: { // 其余属性默认使用全局文本样式，详见TEXTSTYLE
                    fontWeight: 'bolder',
                    fontStyle: 'italic',
                    color: '#000',
                    shadowColor: '#fff', //默认透明
                    shadowBlur: 10
                }
            },
            detail: { //show : true ,
                borderColor: '#fff',
                shadowColor: '#fff', //默认透明
                textStyle: { // 其余属性默认使用全局文本样式，详见TEXTSTYLE
                    fontWeight: 'bolder',
                    fontSize: 14,
                    color: '#333333'
                },
                formatter: '{value}'
            },
            data: [{value: 40, name: '',itemStyle:{color:'#00C3A2'}}]
        }
    
    ]
} //echart 配置项
				            },
		econe:{
					option:{
		    series: [
		        {
		            name: '1',
		            type: 'gauge',
		            center: ['50%', '55%'], // 默认全局居中
		            radius: '100%',
		            min: 0,
		            max: 120,  
		            splitNumber: 10,
		            axisLine: { // 坐标轴线
		                lineStyle: { // 属性lineStyle控制线条样式
		                    color:  [
		                    [1,new this.$echarts.graphic.LinearGradient(0, 0, 1, 0, [
		                      {
		                        offset: 0.1,
		                        color: "#00C3A2"
		                      },
		                      {
		                        offset: 0.6,
		                        color: "#FFF700"
		                      },
		                      {
		                        offset: 1,
		                        color: "#FF2C00"
		                      }
		                    ])
		                  ]
		                ],
		                    width: 5, //半径
		                    shadowColor: '#fff', //默认透明
		                    shadowBlur: 1
		                }
		            },
		            pointer: {
		              width:3,
					  length: '60%'
		            },
		            axisLabel: {
		                //show:false,
		                // 坐标轴小标记
		                textStyle: { // 属性lineStyle控制线条样式
		                    fontWeight: 'bolder',
		                    color: '#999999', //刻度数字颜色 隐藏
		                    shadowColor: '#fff', //默认透明
		                    shadowBlur: 10,
							fontSize: 5
		                }
		            },
		            axisTick: { // 坐标轴小标记
		                length: 5, // 属性length控制线长
		                lineStyle: { // 属性lineStyle控制线条样式
		                    color: '#999999', //坐标轴 小刻度线颜色
							width:1,
		                },
						width:2
		            },
		            splitLine: { // 分隔线
		                length: 5, // 属性length控制线长
		                lineStyle: { // 属性lineStyle（详见lineStyle）控制线条样式
		                    width: 3,
		                    color: 'transparent', //分割线
		                    shadowColor: '#fff', //默认透明
		                    shadowBlur: 10
		                }
		            },
		            title: {
		                textStyle: { // 其余属性默认使用全局文本样式，详见TEXTSTYLE
		                    fontWeight: 'bolder',
		                    fontStyle: 'italic',
		                    color: '#000',
		                    shadowColor: '#fff', //默认透明
		                    shadowBlur: 10
		                }
		            },
		            detail: { //show : true ,
		                borderColor: '#fff',
		                shadowColor: '#fff', //默认透明
		                textStyle: { // 其余属性默认使用全局文本样式，详见TEXTSTYLE
		                    fontWeight: 'bolder',
		                    fontSize: 14,
		                    color: '#333333'
		                },
		                formatter: '{value}'
		            },
		            data: [{value: 50, name: '',itemStyle:{color:'#00C3A2'}}]
		        }
		    
		    ]
		} //echart 配置项
						            }
			}
		},
		computed: {
			// MonitorVersion () {
			// 	return this.$store.state.MonitorVersion
			// }
		},
		onLoad() {
			//this.getech()
			//console.log(option)
		},
		onShow(option) {
			console.log(option)
		},
		methods: {
		getech(){
			var that = this;
			var user = uni.getStorageSync('userinfo')
			that.userId = user.id;
			//console.log(that.userId)
			$http({
				url: '/venus/mobilePhone/stationList',
				data: {
					 userId: that.userId,
					 stationNameOrCode:that.stationNameOrCode
				},
				success(res){
					that.tableData = res.data
					// that.tableData = [{latitude: 32,  //纬度
					// longitude: 118,
					// workStatus:1,
					// id:1,
					// waterFlow:20
					// },
					// {latitude: 36,  //纬度
					// longitude: 118,
					// workStatus:1,
					// id:2,
					// waterFlow:20
					// }]
					// that.ec.option.series[0].max = 50
					// that.ec.option.series[0].
						res.data.map((item,index)=>{
							if(item.workStatus==1){
								that.eachico = that.goodico
							}else{
								that.eachico = that.badico
							}
							 that.marker.push({latitude:item.lat,longitude:item.lon,id:item.id,label:{content:item.stationName},iconPath:that.eachico,workStatus:item.workStatus})
							 //that.marker.push({latitude:32,longitude:118,id:1,label:{content:5555},iconPath:that.eachico,workStatus:1},{latitude:36,longitude:118,id:2,label:{content:5555},iconPath:that.eachico,workStatus:0})
							
							
						})
						that.latitude = that.marker[0].latitude
						that.longitude = that.marker[0].longitude
						
					
				}
			})
			
		},
		mark(e){
			this.show = true;
			
			this.tableData.map((item,index)=>{
				
				if(e.markerId==item.id){
					console.log(item)
					this.longitude = item.longitude;
					this.latitude = item.latitude;
					this.ec.option.series[0].data[0].value=item.waterFlow
					console.log(item.waterFlow)
					this.econe.option.series[0].data[0].value=item.waterPressure
					//console.log(item)
					this.areamessage = item
					//console.log(item)
					this.marker.map((i,index)=>{
						if(i.id==e.markerId){
							//将当前点击的坐标变绿
							i.iconPath= this.nowico;
						}
						else if(i.id!=e.markerId){
							// 地图数组中 没有当前点击的id 那么就通过状态重新判断左边颜色
							if(i.workStatus==0){
								i.iconPath=this.badico
							}
							else if(i.workStatus==1){
								i.iconPath=this.goodico
							}
						}
							
					})
				}
			})
			
		},
		enter(id){
			uni.navigateTo({
				url:'/pages/details/index?id='+id
			})
		},
		report(id){
			//console.log(id)
			uni.navigateTo({
				url:"/pages/report/index?id="+id
			})
		}
			
		},
		mounted() {
			this.getech()
		},
		
	}
</script>

<style lang="less">
	  .start{
		  height: 532rpx;
		
		 //transition: all 0.5s;
	  }
	  .end {
		 
		  //transition: all 0.5s;
		  padding: 0!important;
		  height: 0;
		  .squ{
			  height: 0!important;
		  }
	  }
	.map-legend{
		position: absolute;
		width: 80%;
		left: 50%;
		top: 5%;
		transform: translate(-50%,-50%);
		height: 60rpx;
		background-color: white;
		.map-one {
			float: left;
		}
		.van-icon__image {
			width: 48rpx!important;
			height: 48rpx!important;
			// margin-top: 10rpx;
			
		}
		.txt {
			display: inline-block;
			vertical-align: center;
			line-height: 60rpx;
			margin-left: 20rpx;
		}
	}
	
	.top {
		width: 300px;
		height: 200px;
	}
	.uni-ec-canvas {
		width: 100%;
		height: 100%;
		display: block;
		font-size: 12rpx;
	}
	.box {
		height: 100%;
		overflow: hidden;
		.content {
			 padding: 44px 0 0;
			height: 100%;
			overflow: hidden;
			box-sizing: border-box;
			.divide{
				width: 90%;
				height: 80rpx;
				position: absolute;
				left: 50%;
				top: 45rpx;
				transform: translate(-50%,0);
				.left{
					height: 100rpx;
					width: 100rpx;
					float: left;
					position: relative;
					top: -16rpx;
					image{
						width: 100%;
						height: 100%;
					}
				}
				.right{
					float: left;
					border-radius: 10rpx;
					padding: 0 15rpx;
					//line-height: 80rpx;
					box-sizing: border-box;
					background-color: white;
					image {
						width: 100%;
						height: 100%;
						width: 50rpx;
						height: 50rpx;
					}
					.bad {
						overflow: hidden;
						float: left;
						.tex {
							line-height: 55rpx;
							float: left;
							font-size: 28rpx;
							margin: 0 10rpx;
						}
						.img {
							float: left;
						}
					}
				}
			}
			.bottom {
				transition: all 0.4s;
				padding: 40rpx 30rpx 0 30rpx;
				width: 100%;
				 //height: 532rpx;
				position: absolute;
				bottom: 0;
				left: 0;
				background-color: #FFFFFFFF;
				border-radius: 6px 6px 0 0;
				box-sizing: border-box;
				.pull {
					margin-bottom:35rpx;
					.squ {
						width: 50rpx;
						height: 4rpx;
						background-color: #BBBBBBFF;
						position: relative;
						left: 50%;
						top: 50%;
						transform: translate(-50%,-50%);
						}	
				}
				.area {
					margin-bottom: 22rpx;
					.van-icon--image {
						width: 40rpx;
						height: 40rpx;
						margin-right: 30rpx;
						position: relative;
						left: 0;
						top: 10rpx;
					}
				}
				.watch {
					height: 160rpx;
					border-top: 1px solid #EEEEEEFF;
					display: flex;
					padding-top: 20rpx;
					.mh {
						flex: 1;
						margin-right: 50rpx;
						height: 160rpx;
						.ec-text {
							width: 40%;
							height: 100%;
							font-size: 28rpx;
							color: #666666;
							float: left;
							position: relative;
							.text-bt{
								position: absolute;
								left: 0;
								bottom: 10%;
								font-size: 28rpx;
								line-height: 1.5;
							}
						}
						.ech {
							width: 60%;
							height: 100%;
							float: right;
						}
					}
					.kpa {
							flex: 1;
							margin-left: 50rpx;
							height: 160rpx;
							.ec-text {
								width: 40%;
								height: 100%;
								font-size: 28rpx;
								color: #666666;
								float: left;
								position: relative;
								.text-bt{
									position: absolute;
									left: 0;
									bottom: 10%;
									font-size: 28rpx;
									line-height: 1.5;
								}
							}
							.ech {
								width: 60%;
								height: 100%;
								float: right;
							}
					}
				}
				.local {
					padding: 30rpx 0;
					border-bottom:	1px solid #EEEEEEFF;
					.van-icon--image {
						width: 40rpx;
						height: 40rpx;
						margin-right: 30rpx;
						position: relative;
						left: 0;
						top: 10rpx;
					}
					text {
						color: #666666;
						font-size: 28rpx;
					}
				}
				.exercise{
					padding: 25rpx 0 0 0;
					font-size: 28rpx;
					font-weight: 700;
					.ex-left {
						display: inline-block;
						.van-icon--image {
							width: 40rpx;
							height: 40rpx;
							margin-right: 20rpx;
							position: relative;
							left: 0;
							top: 10rpx;
						}
						
					}
					.ex-right {
						display: inline-block;
						margin-left: 40rpx;
						position: relative;
						.van-icon--image {
							width: 40rpx;
							height: 40rpx;
							margin-right: 20rpx;
							position: relative;
							left: 0;
							top: 10rpx;
						}
					}
				}
			}
		}
	}
</style>
