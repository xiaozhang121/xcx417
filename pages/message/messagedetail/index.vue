<template>
	<view class="box">

		<!-- 切换导航-导航 -->
		<van-nav-bar title="系统消息" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
			<view class="message">
				<view>A站点安居客公交卡的快感克拉里看到过考虑奥地利咖喱阿桑的歌阿迪斯</view>
				<view>2020-04-05 15</view>
			</view>
			<view class="btn">
				<van-button color="linear-gradient(to right, #0068FF, #005AC3)" @click='enter'>处理上报</van-button>
			</view>
		</view>
	</view>
</template>

<script>
	import statusBar from "../../../components/status-bar/index.vue"
	import WatchItem from "../../../components/watch-item/index.vue"
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
		onLoad() {},
		methods: {
			//左上角返回按钮
			onClickLeft() {
				uni.navigateBack();
			},
			enter(){
				uni.navigateTo({
					url: '/pages/report/index'
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
		.content {
			padding: 62px 40rpx 0;
			box-sizing: border-box;	
			.message {
			background-color: #FFFFFF;
				height: 500rpx;
				border-radius: 10rpx;
				padding: 40rpx 30rpx;
				:first-child {
					// font-weight: 700;
					line-height: 2;
				}
				:last-child {
					margin-top: 40rpx;
					font-size: 28rpx;
					color: #999999;
				}

			}
			.btn {
				margin-top: 40rpx;
				.van-button--normal {
					border-radius: 50rpx;
					width: 100%;
				}
			}
		}
		
	}
</style>
