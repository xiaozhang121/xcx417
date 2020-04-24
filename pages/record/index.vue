<template>
	<view class="box">

		<!-- 切换导航-导航 -->
		<van-nav-bar title="上报记录" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
			<scroll-view scroll-y="true" class="sco">
				<view class="list" v-for="item in 18" :key='item' @click="enter">
					<view class="tco">
						<van-icon name="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAAeCAYAAAA7MK6iAAAB3UlEQVRIS9WX207CQBCG/2kJgQBqpASNGm18Aa/UO/XJhCdT79QrX0BWo0YRazCcKqFds1uq9QDdbpTGuWibdjrf/jsz7S5hbIyxfQ46BLAFYCG8/0vnNoALAq/btn0sYpI4XDJWowD658bB65u2XaOx0qM/J0YABH5ADcaOAdqbJRjgJ3TZYG0imp8tGG1qsCs+Y6jE/T9wxbLg+z6c52etCdNSXF5cxNxcSQJbTw663W5ieGJwsVhExSp/AunAE4F/goYjaD620O/3lZUrgzOZDNZWVyYGFvm+ub2TeVcxZfBoNILjOO8xd3e25fXp2XnQHkSwLAuGYahw9dvJ3liXAHZ1rQT66qSkOJfLAQi+M77PMRwOEQVHnwsf132NHUwsWARdXqp+CiRURsHhdeh0/9CE67pT4bHgpWoV+bxQ/GEC7A4G8kYun38fROgxGLh4aDb1wZMqWUy15wXVa5oGstnsN4iocFGQk2yqYqtcRqlUjM3XTw6dThdPkS5IVFxfc5d0BNMqfqpiwyCYppmUJ/09z5MdoDXVvV4PnOv9rsUHpVAo6IG1pCq+FNtOinESu6UHTmOxxzl/SW95m9qCXlRFKluYsBwD5ahxjq3fXuDLnJLYtKEWbtreAOWZAuYf28zLAAAAAElFTkSuQmCC" />
					</view>
					<view class="list-title">
						<view class="title-tp">
							<text class="name">预警上报</text>
							<navigator class="normal" url="/pages/recordDetails/index">
								<view class="ico">
									<van-icon name="arrow" color='#BBBBBB'/>
								</view>
							</navigator>
						</view>
						<view class="title-bd">
							2020.03.30 12:01:25
						</view>
					</view>
				</view>
			</scroll-view>
			<view class="fxbtn">
				<van-button color="linear-gradient(to right, #0068FF, #005AC3)" @click='nav'>数据采集上报</van-button>
			</view>
		</view>
	</view>
</template>

<script>
	import statusBar from "../../components/status-bar/index.vue"
	import WatchItem from "../../components/watch-item/index.vue"
	export default {
		name: "user",
		components: {
			statusBar,
			WatchItem
		},
		data() {

		},
		computed: {},
		onLoad() {},
		methods: {
			//左上角返回按钮
			onClickLeft() {
				uni.navigateBack()
			},
			nav(){
				   uni.navigateTo({
				            url:"/pages/report/index"
				        })
			},
			enter(){
				uni.navigateTo({
					url: "/pages/recordDetails/index"
				})
			}
				

		},
		mounted() {},

	}
</script>

<style lang="less">
	.sco {
		background-color: #F3F3F3;
		padding-bottom: 90rpx;
	}
	.box {
		 height: 100%;
		background-color: #F3F3F3;
	
		.content {
			padding: 44px 0 0;
			box-sizing: border-box;
			.list {
				border-radius: 10rpx;
				border: 1px solid white;
				background-color: white;
				margin-bottom: 15rpx;
				padding: 30rpx;
				font-size: 28rpx;
				position: relative;
				margin-top: 20rpx;
				.tco {
					position: absolute;
					top: 48rpx;
					.van-icon--image {
						width: 60rpx;
						height: 60rpx;
						
					}
				}
				.list-title {
					margin-left: 110rpx;
					position: relative;
					.title-tp {
						margin-bottom: 15rpx;
						position: relative;
						.normal {
							position: absolute;
							right: 0;
							top: 60%;
							.ico {
								// position: absolute;
								// top: 2rpx;
								// right: 0rpx;
								// color: #BBBBBBFF;
								// .van-icon--image {
								// 	width: 16rpx;
								// 	height: 28rpx;
									
								// }
							}
						}
						.name {
							font-size: 32rpx;
							font-weight: 700;
							color: #333333;
							font-family: PingFang SC;
						}
					}
					.title-bd {
						color: #666666FF;
					}
				}
			}
			.fxbtn {
				position: fixed;
				left: 0;
				bottom: 0;
				width: 100%;
				.van-button--normal{
					width: 100%;
				}
			}
		}
	}
</style>
