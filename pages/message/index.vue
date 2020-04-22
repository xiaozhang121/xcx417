<template>
	<view class="box">

		<!-- 切换导航-导航 -->
		<van-nav-bar title="消息通知" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
			
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
		return {
		
		}
		},
		computed: {},
		onLoad() {},
		methods: {
			//左上角返回按钮
			onClickLeft() {
				uni.navigateBack();
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
			
		}
		
	}
</style>
