<template>
	<view class="box">

		<!-- 切换导航-导航 -->
		<van-nav-bar title="系统消息" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
			<view class="message">
				<view>{{tableData.datail}}</view>
				<view>{{tableData.publishTime}}</view>
			</view>
			<view class="btn">
				<van-button color="linear-gradient(to right, #0068FF, #005AC3)" @click='enter(tableData.id)'>处理上报</van-button>
			</view>
		</view>
	</view>
</template>

<script>
	import statusBar from "../../../components/status-bar/index.vue"
	import WatchItem from "../../../components/watch-item/index.vue"
	import {$http} from "../../common/util.js"
	export default {
		name: "user",
		components: {
			statusBar,
			WatchItem
		},
		data() {
		return {
			id:'',
			tableData:{}
		}
		},
		computed: {},
		onLoad(option) {
			console.log(option)
			this.id = option.id
			this.getmessageDetail()
		},
		methods: {
			//左上角返回按钮
			onClickLeft() {
				uni.navigateBack();
			},
			enter(id){
				uni.navigateTo({
					url: '/pages/alarm/alarmreport/index?id'+id
				})
				
			},
			getmessageDetail(){
				var that = this;
				$http({
					url: '/venus/mobilePhone/messageDetail',
					data: {
						id:that.id
					},
					success(res){
						console.log(res)
						// that.user = res.data.username;
						// that.id = res.data.id;	
						// console.log(that.tableData)
						that.tableData = res.data
					}
				})
			},
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
