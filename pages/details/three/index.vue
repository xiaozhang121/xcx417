<template>
	<view class="">
		<view class="choose">
			<view class="choose-time" v-for="(item,index) in choose" @click="sele(item,index)" :class="currentindex===index?'select':''" :key='index'>
				{{item}}
			</view>
		</view>
		
			<view class="card">
				<view class="list" v-for="(item,index) in tableData" :key='index'>
					<view class="list-title">
						<view class="title-tp">
							<text class="name">{{item.alarmTime}}</text>
							<text class="normal">{{item.alarmType==1?'爆管':'泄露'}}</text>
						</view>
					</view>
					<view class="list-main">
						<view class="main-tp">
							<text>流量: {{item.flowValue}}</text>
							<text>压力: {{item.pressureValue}}</text>
						</view>
						<view class="main-tp">
							<text>站点状态: {{item.stationStatus}}</text>
							<text>阀门状态: {{item.valve}}</text>
						</view>
						<view class="main-bd">
							报警描述: {{item.alarmInfo}}
						</view>
					</view>
				</view>
			</view>
		
	</view>
</template>

<script>
	 import {$http} from "../../common/util.js"
	export default {
		data(){
			return {
			choose: ['全部','爆管','泄露','无信号'],
			currentindex:1,
			pageIndex:1,
			pageRows:3,
			tableData:[],
			}
		},
		props:['getmore'],
		watch:{
			getmore(){
				//console.log(1);
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
			}
		},
		mounted(){
			this.gethistory()
		},
			methods: {
			sele(item,e){
				if(this.currentindex==e){
					return;
				}
				this.currentindex = e;
				this.type = item;
				this.tableData.length=0
				this.pageIndex=1;
				this.gethistory();
				
				
			},
			gethistory(){
				var that = this;
				if(that.currentindex==2){
					that.currentindex=15
				}
				$http({
					url: '/venus/mobilePhone/historyAlarm',
					data: {
						pageIndex:that.pageIndex,
						pageRows:that.pageRows,
						type:that.currentindex
					},
					success(res){
						console.log(res)
						//console.log(res.data)
						// that.tableData = res.data.tableData
						// console.log(that.tableData)
						//合并消息页
						that.tableData = [...that.tableData, ...res.data.tableData];
						that.totalRows = res.data.pageParam.totalRows;
						
					}
				})
			}
		
			
		},
	}
</script>

<style lang="less">
	.uni-ec-canvas {
		width: 100%;
		height: 100%;
		display: block;
	}
	.choose {
		padding: 36rpx 100rpx;
		background-color: rgb(243, 243, 243);
		display: flex;
		.choose-time {
			font-size: 28rpx;
			height: 56rpx;
			background-color: #CCCCCC;
			flex: 1;
			text-align: center;
			margin-right: 20rpx;
			line-height: 56rpx;
			border-radius: 30rpx;
			color: #FFFFFF;
			}
			.select {
				background-color: #005AC3;
			}
			view:nth-child(5) {
					margin-right: 0;
		}
	}
	.card {
		background-color: rgb(243, 243, 243);
		.list {
			border-radius: 10rpx;
			border: 1px solid white;
			background-color: white;
			margin-bottom: 15rpx;
			padding: 30rpx;
			font-size: 28rpx;
			.list-title {
				border-bottom: 1px solid rgb(239, 239, 239);
				.van-icon{
					position: absolute!important;
					right: 5rpx;
				}
				.title-tp {
					margin-bottom: 30rpx;
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
					color: #666666FF;
					margin-bottom: 30rpx;
				}
			}
			.list-main {
				margin: 20rpx 0;
				.main-tp {
					margin-bottom: 15rpx;
					color: #666666FF;
					text:first-child{
						margin-right: 75rpx;
					}
				}
				.main-bd {
					color: #999999FF;
				}
			}
		}
	}
</style>
