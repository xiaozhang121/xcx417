<template>
	<view class="box">

		<!-- 切换导航-导航 -->
		<van-nav-bar title="监测站点" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
			<view class="search">
				<van-search placeholder="请输入搜索关键词" use-action-slot @change="onChange" @search="onSearch">
					<view slot="action" bind:tap="onClick" class="se-btn" @click="onSearch">搜索</view>
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
				tableData:[],
				userId:'',
				name:'',
				stationNameOrCode:'',
				pageIndex:1,
				pageRows:7,
				totalRows:10,
				totalPages:1
			}
		},
		onReachBottom(){
			// if(this.totalPages<=this.pageIndex){
			// 	uni.showToast({
			// 		title:'没有更多数据了',
			// 		icon:'none'
			// 	})
			// 	return false;
			// }
			// this.pageIndex++
			// this.pageRows = this.pageIndex*this.pageRows
			// this.getwatch()
			
			if (this.tableData.length >= this.totalRows) {
			  // 没有更多数据了，给一个提示，终止后续的接口调用
			  uni.showToast({
			    title: '没有更多数据了',
				icon:'none'
			  })
			  return
			}
			// 加载下一页数据
			this.pageIndex = this.pageIndex + 1
			// 页码加一后需要再次调用后台接口
			this.gethistory()
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
			onChange(e){
				this.stationNameOrCode = e.detail;
				//this.getwatch()
			},
			getwatch(){
				var that = this;
				var user = uni.getStorageSync('userinfo')
				that.userId = user.id;
				//console.log(that.userId)
				$http({
					url: '/venus/mobilePhone/stationList/ByPage',
					data: {
						 pageIndex:that.pageIndex,
						 pageRows:that.pageRows,
						 userId: that.userId,
						 stationNameOrCode:that.stationNameOrCode
						 //stationNameOrCode:003
					},
					success(res){
						console.log(res)
						// that.user = res.data.username;
						// that.id = res.data.id;	
						//  that.tableData = res.data.tableData
						//  //that.name = res.data.tableData.stationName
						// // console.log(that.tableData)
						// that.totalRows = res.data.pageParam.totalRows
						// that.totalPages = res.data.pageParam.totalPages
						
						that.tableData = [...that.tableData, ...res.data.tableData];
						that.totalRows = res.data.pageParam.totalRows;
					}
				})
				
			},
			reachBottom(){
				console.log(1)
				this.pageIndex++;
				this.getwatch();
			},
			onSearch(){
				this.getwatch()
			}

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
