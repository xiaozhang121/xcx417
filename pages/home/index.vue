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
			<map style="width:100%;height:100vh;":latitude="latitude":longitude="longitude" :markers="marker"></map>
			<view class="bottom" v-if="false">
				<view class="pull">
					<view class="squ">
					</view>
				</view>
				<view class="area">
					<van-icon name="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAABrklEQVRIS82UvTIDURTHfydFUhgzSjTkCSQNSSUaSyWegPRMqJQoVdbQ8waiskkjqoRG8gSiQZnKR2bkmisybHbv7s6YzDjl3bPnd/7nSxiyyZDj8w8Ad1djdDpFFHkg9a24gVAiHj8ivdAOqkKwgptyHsUpMGYI0kYoMGeVTBAzoBf8PFKPhFUTxB+gy/LeuQ/IfJDbJhFP+pXLH1B3tkAOfbJvfr/NeL+pbTJL9uC7AVBuAO4gSgpkF8++AtQq64jSvfltDTJWOipAuRwV12StnOut7pNExvIkbFIQDqiVqwjzLmhkQM1pITLl+jkmaWYXdengtpKiq+5CVYJhk+uODVL0aXJ/3vXSuU2xT9bai9aD2uU0EtNjGt1UN0l2uRUN8DUp5T2E3UgEQ/b63+BTUXdKICshkCYZq3+jPK7BgN5GVz078ROmSSKeCzp44edaQ946NsLaQFcvSCTW/3ZNdcTjgzyiikxO5Jgc7zEen+HxqYqSIzZ3jJc0vAfa4+RAT0ZvJ0ZH4KMLL699MQ9s7EwH9Si8RFoBbHm2Vp8PsP+uINKcmp3CFfx3wCdrRoMZxJibEgAAAABJRU5ErkJggg==" />
					<text>站点C</text>
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
							   class="uni-ec-canvas"
							   id="uni-ec-canvas"
							   ref="uni-ec-canvas"
							   canvas-id="uni-ec-canvas"
							   :ec="ec"
							></uni-ec-canvas>
						</view>
					</view>
				</view>
				<view class="local">
					<van-icon name='data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABQAAAAUCAYAAACNiR0NAAABPElEQVQ4T72UwVEDMQxFJTVAOoBUAOmAEkIFhMtqfaSChA64eXxaqIB0AB0QKiBUwHLNQWKc8TLGsdkNk4lvO5aev/SlRTjwwQPz4LhAa+0ZIs4RcQoAIwBoVXWpqnfGmHWuuqJCa+0lET0FUJrbisiVMeYlvcgCvTIiek1gHwBwGgE8dJIqzQKdcw8AcO2TVfVNVac+MbRgiYjnAfzIzLNYZQno+7NVg4iTqqpWXVJoxXN4bF3X9XgIULsgZv71aNM0o81m81m6LylsAeDEJ4nIjTHGt2B7rLUzImrC5xcze/d/Tm8Pw6gsiGglIheIuIjMGtbD4PJ73xaJyHiQy5nSdthpK7qAP1fPOefLm2eU3jLz/V6b0gXHM1mavV5T0pcj6I4Jg1YvV4ofl3h8SoYd9/fVNzb/MmVf6DcBtocVrvnaNQAAAABJRU5ErkJggg=='></van-icon>
					<text>地理位置: 甘肃省陇南市</text>
				</view>
				<view class="exercise">
					<view class="ex-left">
						<van-icon name='data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABQAAAAUCAYAAACNiR0NAAABP0lEQVQ4T92UwVHDQAxFVzr4SkqACnAHOBUwrgB8sewToQKGCkhO3vXFdBBTAdBBqABKcK57kBgxzoxJHJOEnLKn3Vnpjf6XRmCOfODIPHMCwKqqRt77V7UmCIJxkiTNkE2DksuyDJl5DgDnChGRL0SM0zRdbINuBRZFESHi3BgzWktumDnO8/ytD9oLLIriFhGrIWnMnOR5/rweswF0zmnQzSpQRF5EZKpvAJgAwHUHMiWi+y60D6imn7VB70QUOecmIiJZls2ccyr1qv1fEtEvS3olO+ekTXhkZm3Ej3xmHiNiZIx50DcRbeQPAkVkJiI1IurYLJk5bGXfHQQ0xjRBEFx0PfLef646v3eFLagmoljv1tq625RDgTrQ2l2156lb7c5Aa+0CAC6H5lBEPrIsC/+cw/+usxNYX/ta8A2QsYQVMYlVfgAAAABJRU5ErkJggg=='></van-icon>
						<text>查看详情</text>
					</view>
					<view class="ex-right">
						<van-icon name='data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABQAAAAUCAYAAACNiR0NAAABCUlEQVQ4T+2TsW3DMBBF/7GQWmeCJBPEniDJCBlBjU7qPEKyQTqKlTJCNrC9gbKBsoFrFXcGDVMQDJmKEVVBCBDggXfv/n2QhJkXzczDHwFaa++IaGOMecnzvInZNDlyXdeLrus2AJaq2qZpusqybH8JGgUOYQNAkyTJ8yVoFFhVVUNEDyNqGmZejamcHNkXWWufjDF+7Ddmfv2Vh7MAT4oePUxEvgG0QaGI+PPtSeUXM38OFY+O7JxrAYSiHRGtVfUdgN9rAMdmAPbMfBMFDvzq81R1GwIiWgJYhFhEsrIsP/r7c4Odc744KJj86v5tFkVxHwPqJOUsgZl76370bK5p8A+8xq3x3AM+WFsVRHGfxgAAAABJRU5ErkJggg=='></van-icon>
						<text>数据上报</text>
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
				latitude: 40.013305,  //纬度
				longitude: 118.685713,  //经度
				marker: [{
				   　　id:0,
				   　　latitude: 40.013305,//纬度
				   　　longitude: 118.685713,//经度
				   　　iconPath: '',    //显示的图标        
				   　　rotate:0,   // 旋转度数
				   　　width:20,   //宽
				   　　height:20,   //高
				  　　 title:'你在哪了',//标注点名
				  　　 alpha:0.5,   //透明度
				  　　 label:{//为标记点旁边增加标签   //因背景颜色H5不支持
				  　　 content:'站点A',//文本
				　　　　color:'#333'//文本颜色
				       // 　　fontSize:24,//文字大小
				       //    x:5,//label的坐标，原点是 marker 对应的经纬度
				       //    y:1,//label的坐标，原点是 marker 对应的经纬度 
				       //    borderWidth:12,//边框宽度
				       //    borderColor:'pink',//边框颜色    
				       // 　　borderRadius:20,//边框圆角                        
				       // 　　bgColor:'black',//背景色
				       // 　　padding:5,//文本边缘留白
				       //    textAlign:'right'//文本对齐方式。
				   },
				   callout:{//自定义标记点上方的气泡窗口 点击有效  
				   　　content:'幸福花园店A组',//文本
				   　　color:'#ffffff',//文字颜色
				   　　fontSize:14,//文本大小
				   　　borderRadius:2,//边框圆角
				  　　 bgColor:'#00c16f',//背景颜色
				   　　display:'ALWAYS',//常显
				   },
				   // anchor:{//经纬度在标注图标的锚点，默认底边中点
				   //     x:0,    原点为给出的经纬度
				   //     y:0,
				   // }
				                
				   }],
				userId:'',
				stationNameOrCode:'',
				ec:{
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
            data: [{value: 40, name: '',itemStyle:{color:'#00C3A2'}}]
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
			this.getech()
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
					console.log(res)
					//that.ec.option.series[0].max = 50
					// that.ec.option.series[0].
				}
			})
			
		},
			
		},
		mounted() {
			this.getech()
		},
		
	}
</script>

<style lang="less">
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
		.content {
			padding: 62px 0 0;
			height: 100%;
			box-sizing: border-box;
			
			.bottom {
				padding: 40rpx 30rpx 0 30rpx;
				width: 100%;
				height: 532rpx;
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
