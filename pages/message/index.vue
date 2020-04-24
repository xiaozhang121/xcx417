<template>
	<view class="box">

		<!-- 切换导航-导航 -->
		<van-nav-bar title="消息通知" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
			<scroll-view scroll-y="true" class="sco" >
				<view class="list"  v-for="item in 15" :key='item' @click="enter">
					<view class="tco">
						<van-icon dot name="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAAeCAYAAAA7MK6iAAABmUlEQVRIS+2X307CMBTGv47BRiQOEvBOccEoXLk3UJ/M8WTiG/gC0JFIght/SjK4gEFNJxAShnM4tpjYizVZ2vPrd9qcfIdgPSiljxzkGYABoLj5H9PMALwR8Kau6y0Rk4hPm1KTfEFPPjh4s6brJlkrfTk5cQdAwJ9Ih9IWQB6SBAP8lbQ7lBFCtGTBYKRDLZ4w1Mf9g/eyXimXUSicRb4N13XhDIYH94WmWr+uRoZui5LV/cPg+XwO23FC1V9UKsjlcv46Godiallw3WkoOJ9XcVOrxQcOJQYsiEVxauB+/wNWN/iVqooCw7jfO1ssiqezGcQDCxoSkaBp56cBp5bqxMFFTUOpFN0JjccMbDI5vnIxxiBnMpBl2Q/SaNS3wQaDIZyAouJ5HrzlEsXi4QOH1mpBWSwWWK1WPrB+d+vPAvre60FV1T1VkiQhm81+ezs/Au9GqF5dYjQa+1BNO964RAbbtg1FUX4FFUIig4953UF7UjF7nPNJevY2NUMv8p9KC7P1R37TBpNzGHEbfP9OiWjaYG6atk+aHPTXiNgrMAAAAABJRU5ErkJggg=="  />
					</view>
					<view class="list-title">
						<view class="annouce">
							预警公告
						</view>
						<view class="title-tp" >
							<text class="name">XXX处发生泄漏</text>
							<navigator class="normal">
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
		</view>
	</view>
</template>

<script>
	import statusBar from "../../components/status-bar/index.vue"
	import WatchItem from "../../components/watch-item/index.vue"
	import {$http} from "../common/util.js"
	export default {
		name: "user",
		components: {
			statusBar,
			WatchItem
		},
		data() {
		return {
		
		}
		},
		computed: {},
		onLoad() {
			this.getmessage()
		},
		methods: {
			//左上角返回按钮
			onClickLeft() {
				uni.navigateBack();
			},
			enter() {
				uni.navigateTo({
					url:'/pages/message/messagedetail/index'
				})
			},
			getmessage(){
				var that = this;
				var {id} = uni.getStorageSync('userinfo')
				console.log(id)	
				$http({
					url: 'https://nei.netease.com/api/apimock-v2/e64ee4e782c695855b9f3645456ae8ce/venus/mobilePhone/message',
					data: {
						 pageIndex:that.pageIndex,
						 pageRows:that.pageRows,
						 userId: id
					},
					success(res){
						console.log(res)
						// that.user = res.data.username;
						// that.id = res.data.id;	
						// that.tableData = res.data.tableData	
						// console.log(that.tableData)
					}
				})
			}
		},
		mounted() {},

	}
</script>

<style lang="less">
	.sco {
		background-color: #F3F3F3;
	}
	.box {
		height: 100%;
		background-color: #F3F3F3;
		.search {
			width: 100%;

			.van-search__field {
				border: 1px solid rgb(209, 209, 209);
				color: rgb(209, 209, 209);
				border-radius: 20px;
				padding-left: 60rpx;
			}

			.se-btn {
				margin-left: 60rpx;
				margin-right: 30rpx;
				font-size: 32rpx;
				color: #005AC3FF;
			}
		}

		.content {
			padding: 42px 0 0;
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
					top: 34%;
					.van-icon--image {
						width: 60rpx;
						height: 60rpx;
						
					}
				}
				.list-title {
					margin-left: 110rpx;
					position: relative;
					.annouce {
						margin-bottom: 15rpx;
						color: #666666;
					}
					.title-tp {
						margin-bottom: 15rpx;
						position: relative;
						.normal {
							position: absolute;
							right: 0;
							top: 0;
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
			
		}
		
	}
</style>
