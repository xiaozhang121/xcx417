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
			<view class="bottom">
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
						<uni-ec-canvas
						   class="uni-ec-canvas"
						   id="uni-ec-canvas"
						   ref="uni-ec-canvas"
						   canvas-id="uni-ec-canvas"
						   :ec="ec"
						></uni-ec-canvas>
					</view>
					<view class="kpa">
						<uni-ec-canvas
						   class="uni-ec-canvas"
						   id="uni-ec-canvas"
						   ref="uni-ec-canvas"
						   canvas-id="uni-ec-canvas"
						   :ec="ec"
						></uni-ec-canvas>
					</view>
				</view>
				<view class="local">
					<van-icon name='data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABQAAAAUCAYAAACNiR0NAAABPElEQVQ4T72UwVEDMQxFJTVAOoBUAOmAEkIFhMtqfaSChA64eXxaqIB0AB0QKiBUwHLNQWKc8TLGsdkNk4lvO5aev/SlRTjwwQPz4LhAa+0ZIs4RcQoAIwBoVXWpqnfGmHWuuqJCa+0lET0FUJrbisiVMeYlvcgCvTIiek1gHwBwGgE8dJIqzQKdcw8AcO2TVfVNVac+MbRgiYjnAfzIzLNYZQno+7NVg4iTqqpWXVJoxXN4bF3X9XgIULsgZv71aNM0o81m81m6LylsAeDEJ4nIjTHGt2B7rLUzImrC5xcze/d/Tm8Pw6gsiGglIheIuIjMGtbD4PJ73xaJyHiQy5nSdthpK7qAP1fPOefLm2eU3jLz/V6b0gXHM1mavV5T0pcj6I4Jg1YvV4ofl3h8SoYd9/fVNzb/MmVf6DcBtocVrvnaNQAAAABJRU5ErkJggg=='></van-icon>
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
	
	export default {
		name: "user",
		components: { 
			statusBar,
			WatchItem,
			 uniEcCanvas
		},
		data() {
			return{
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
            data: [
                { value: 40 }
            ]
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
		onLoad() {},
		methods: {
		
			
		},
		mounted() {},
		
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
	.ech {
		width: 100%;
		height: 300px;
	}
	.box {
		.content {
			padding: 62px 0 0;
			height: 100%;
			box-sizing: border-box;
			
			.bottom {
				padding: 40rpx 30rpx 0 30rpx;
				width: 100%;
				height: 512rpx;
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
					.mh {
						flex: 1;
						border: 1px solid #333;
						margin-right: 50rpx;
						height: 160rpx;
					}
					.kpa {
							flex: 1;
							border: 1px solid #333;
							margin-left: 50rpx;
							height: 160rpx;
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
				}
				.exercise{
					padding: 25rpx 0 0 0;
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
