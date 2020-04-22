<template>
	<view class="box">
		<!-- 切换导航-导航 -->
		<van-nav-bar title="监测站点" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
			<van-tabs :active="active" @change="onChange">
			  <van-tab title="站点详情">
				<one></one>
			  </van-tab>
			  <van-tab title="历史记录">
				  <two></two>
			  </van-tab>
			  <van-tab title="历史报警">
				  <three></three>
			  </van-tab>
			</van-tabs>
		</view>
	</view>
</template>

<script>
	import statusBar from "../../components/status-bar/index.vue"
	import WatchItem from "../../components/watch-item/index.vue"
	import one from "./one/index.vue"
	import two from "./two/index.vue"
	import three from "./three/index.vue"
	export default {
		name: "user",
		components: {
			statusBar,
			WatchItem,
			one,
			two,
			three
		},
		data() {
		return {
			active: 0
		}
		},
		computed: {},
		onLoad() {},
		methods: {
			//左上角返回按钮
			onClickLeft() {
				uni.navigateBack()
			},
			onChange(){
				
			}

		},
		mounted() {},

	}
</script>

<style lang="less">
	.uni-ec-canvas {
		width: 100%;
		height: 200px;
		display: block;
		font-size: 12rpx;
	}
	.van-icon--image {
		width: 48rpx!important;
		height: 48rpx!important;
		margin-top: 20rpx;
		margin-right: 20rpx;
		float: right;
	}
	.box {
		height: 100%;
		.content {
			padding: 42px 0 0;
			height: 100%;
			.van-sticky{
				padding: 0 120rpx;
				.van-tabs__line {
					background-color: #005AC3;
				}
				.van-tab--active {
					color:#005AC3;
					// font-size: 32rpx;
					font-weight: 700;
				}
			}

		}
	}
</style>
