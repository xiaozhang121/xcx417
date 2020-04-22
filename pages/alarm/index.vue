<template>
	<view class="box">

		<!-- 切换导航-导航 -->
		<van-nav-bar title="监测站点" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
			<view class="search">
				<van-search placeholder="请输入预警类别、地理位置" use-action-slot bind:change="onChange" bind:search="onSearch">
					<view slot="action" bind:tap="onClick" class="se-btn">搜索</view>
				</van-search>
			</view>
			<date-time></date-time>
			<view class="card">
				<view class="list" v-for="(item,index) in 5" :key='index'>
					<view class="list-title">
						<view class="title-tp">
							<text class="name">2020.03.29 12:11:42</text>
							<text class="normal">爆管</text>
						</view>
						<view class="title-bd">
							<text>流量: 735^3/h</text>
							<text>压力: 5kPa</text>
						</view>
					</view>
					<view class="list-main">
						<view class="main-tp">
							<text>站点名称: 南京六合站</text>
						</view>
						<view class="main-tp">
							<text>地理位置: 南京六合站</text>
						</view>
						<view class="main-tp">
							<text>阀门描述: </text>
						</view>
						<view class="main-bd">
							<text>预警描述: </text>
						</view>
						<view class="ico">
							<van-icon name="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAACbElEQVRIS62WP0xTURTGf+d10QXrpOAgLoJKAi6OkGjUkaqJuqhlUBMJ/plMHBQdjE5GCCbGodVNErRMRl1gdZEmgDjJYtENcVAHesx5ty3l8e6zNbzkLfee+333fOffFRK+T0varkp/GTKipBF6QnNlRoXlAAoiTO5rlUUfjMRtGHC5zB2EbNIFantKPgi4G0e0gWC+pJmykhMh3RB4xUiV5UAY2N8mhfpz6whmlzQrSq4Z4KitCgNdrZKvrtcINgO8DvRE1ZOQwDRfLfOxWVl8nppcqYCDFpOQYLakeYELcQdWfsHD97Dwzf2dO91/8yi0bPWLqfC8q02yEmaM8iXO9MMiXBuHld8bd1u2wOPTcKjdTxIIe2S+pNcVHkXN7ObHRx344b0w2AedrfB1GQpFeDINRvJ2yO+JwA2ZLemUQF+U4NYkTBYd+OjZjbccm3Yk/d1wvz/eC4VpmSupVeHuqMnJp/D5O0xcdDePfgtLcOqZi8fEJY9MyowRaNz2gXtude62X+NGbLwEjXrQsQNeXfZfwitRNQZHOmDkzH/GQCl6g2xZdGwEfv4BI7nSu5ZFFvyxKUil4M0g7NqeEGRfmtoRq4OrLx1J9EsJrKoLcu5cfKqGaZpUaAZqnjx456rYsso0N9DBXhgad2s+krDQ/tUq/OFz5NkXjsQqOnd+zbrWKmwpbHaWs7AtCdDXq4zEqjpf6WYKP1JCT63Z2UEbNAqvmyWIsxdY366rRpsxE7wDp0oSjkyw9t2UXCZLANnEkVklqcRk2DcjorJYQFPCcENDv/5w5dliHmVQ0iJ0274qRdaeLYWkZ8tfRVkVrJbBytQAAAAASUVORK5CYII=" />
						</view>
					</view>
					<view class="list-bt" @click="navi">
						处理上报 →
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import statusBar from "../../components/status-bar/index.vue"
	import WatchItem from "../../components/watch-item/index.vue"
	import DateTime from "../../components/datetime/index.vue"
	export default {
		name: "user",
		components: {
			statusBar,
			WatchItem,
			DateTime
		},
		data() {
		return {
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
			}
		}
		},
		computed: {},
		onLoad() {},
		methods: {
			//左上角返回按钮
			onClickLeft() {
				uni.navigateBack();
			},
			navi(){
				uni.navigateTo({
					url: "/pages/alarm/alarmreport/index"
				})
			}

		},
		mounted() {},

	}
</script>

<style lang="less">
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
			.card {
				background-color: rgb(243, 243, 243);
				margin-top: 20rpx;
				.list {
					border-radius: 10rpx;
					border: 1px solid white;
					background-color: white;
					margin-bottom: 15rpx;
					padding: 30rpx 30rpx 20rpx;
					 font-size: 28rpx;
					.list-title {
						border-bottom: 1px solid rgb(239, 239, 239);
						.van-icon{
							position: absolute!important;
							right: 5rpx;
						}
						.title-tp {
							margin-bottom: 20rpx;
							position: relative;
							.ico {
								position: absolute;
								top: 2rpx;
								right: 0rpx;
								color: #BBBBBBFF;
							}
							.name {
								font-size: 36rpx;
								color: #333333;
								font-weight: 700;
							}
							.normal {
								float: right;
								margin-right: 60rpx;
								color: #FF0000;
							}
						}
						.title-bd {
							margin-bottom: 20rpx;
							color: #666666FF;
							text:first-child {
								margin-right: 100rpx;
							}
						}
					}
					.list-main {
						margin: 20rpx 0;
						position: relative;
						.main-tp {
							margin-bottom: 15rpx;
							color: #666666FF;
							text:first-child{
								margin-right: 75rpx;
							}
						}
						.main-bd {
							color: #666666FF;
							padding-bottom: 20rpx;
							border-bottom: 1px solid rgb(239, 239, 239);
						}
						.ico {
							position: absolute;
							right: 0;
							top: 30%;
							.van-icon--image {
								width: 36rpx;
								height: 36rpx;
							}
						}
					}
					.list-bt {
						text-align: center;
						color: #0068FF;
						margin-top: 20rpx;
					}
				}
			}
		}
		
	}
</style>
