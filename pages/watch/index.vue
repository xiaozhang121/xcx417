<template>
	<view class="box">

		<!-- 切换导航-导航 -->
		<van-nav-bar title="监测站点" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
			<view class="search">
				<van-search placeholder="请输入搜索关键词" use-action-slot bind:change="onChange" bind:search="onSearch">
					<view slot="action" bind:tap="onClick" class="se-btn">搜索</view>
				</van-search>
			</view>
			<scroll-view scroll-y="true" class="body">
			<!-- 	<view class="body" @click="enter"> -->
					<watch-item :receive='tableData' @scrolltolower='reachBottom' :style="{height:scrollH+'px'}" :lower-threshold="0"></watch-item>
				<!-- </view> -->
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
			WatchItem,
			
		},
		data() {
			return {
				pageIndex:1,
				pageRows:5,
				tableData:[]
			}
		},
		computed: {},
		onLoad(option) {
			this.getwatch(),
			console.log(option)
		},
		methods: {
			//左上角返回按钮
			onClickLeft() {
				uni.navigateBack();
			},
			enter(){
				uni.navigateTo({
					url:'/pages/details/index'
				})
			},
			getwatch(){
				var that = this
				$http({
					url: 'https://nei.netease.com/api/apimock-v2/e64ee4e782c695855b9f3645456ae8ce/venus/mobilePhone/stationList/ByPage?userId=&stationNameOrCode=&pageIndex=&pageRows=',
					data: {
						 pageIndex:that.pageIndex,
						 pageRows:that.pageRows,
						 userId: '22'
					},
					success(res){
						//console.log(res)
						// that.user = res.data.username;
						// that.id = res.data.id;	
						that.tableData = res.data.tableData	
						console.log(that.tableData)
					}
				})
				
			},
			reachBottom(){
				console.log(1)
				this.pageIndex++;
				this.getwatch();
			},

		},
		mounted() {},

	}
</script>

<style lang="less">
	.eca {
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
background-color: rgb(243, 243, 243);
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
			
			// .scroll-Y {
			// 	background-color: rgb(243, 243, 243);

			// }

			.body {
				box-sizing: border-box;
				height: 100%;
				padding: 10rpx 25rpx 0 25rpx;
			}
		}
	}
</style>
