<template>
	<view class="box">

		<!-- 切换导航-导航 -->
		<van-nav-bar title="预警" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
			<view class="search">
				<van-search placeholder="请输入预警类别、地理位置" use-action-slot @change="onChange" >
					<view slot="action" @tap="onClick" class="se-btn">搜索</view>
				</van-search>
			</view>
			<date-time @starttime="starttime" @endtime = "endtime"></date-time>
			<scroll-view scroll-y="true" class="card" @scrolltolower='reachBottom' :style="{height:scrollH+'px'}">
					<view class="list" v-for="(item,index) in tableData" :key='index'>
						<view class="list-title">
							<view class="title-tp">
								<text class="name">{{item.alarmTime}}</text>
								<text class="normal">{{item.alarmType}}</text>
							</view>
							<view class="title-bd">
								<text>流量: {{item.flowValue}}/h</text>
								<text>压力: {{item.pressureValue}}pa</text>
							</view>
						</view>
						<view class="list-main">
							<view class="main-tp">
								<text>站点名称: {{item.stationName}}</text>
							</view>
							<view class="main-tp">
								<text>地理位置: {{item.address}}</text>
							</view>
							<view class="main-tp">
								<text>阀门描述: {{item.valve}}</text>
							</view>
							<view class="main-bd">
								<text>预警描述: </text>
							</view>
							<view class="ico">
								<van-icon name="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAACbElEQVRIS62WP0xTURTGf+d10QXrpOAgLoJKAi6OkGjUkaqJuqhlUBMJ/plMHBQdjE5GCCbGodVNErRMRl1gdZEmgDjJYtENcVAHesx5ty3l8e6zNbzkLfee+333fOffFRK+T0varkp/GTKipBF6QnNlRoXlAAoiTO5rlUUfjMRtGHC5zB2EbNIFantKPgi4G0e0gWC+pJmykhMh3RB4xUiV5UAY2N8mhfpz6whmlzQrSq4Z4KitCgNdrZKvrtcINgO8DvRE1ZOQwDRfLfOxWVl8nppcqYCDFpOQYLakeYELcQdWfsHD97Dwzf2dO91/8yi0bPWLqfC8q02yEmaM8iXO9MMiXBuHld8bd1u2wOPTcKjdTxIIe2S+pNcVHkXN7ObHRx344b0w2AedrfB1GQpFeDINRvJ2yO+JwA2ZLemUQF+U4NYkTBYd+OjZjbccm3Yk/d1wvz/eC4VpmSupVeHuqMnJp/D5O0xcdDePfgtLcOqZi8fEJY9MyowRaNz2gXtude62X+NGbLwEjXrQsQNeXfZfwitRNQZHOmDkzH/GQCl6g2xZdGwEfv4BI7nSu5ZFFvyxKUil4M0g7NqeEGRfmtoRq4OrLx1J9EsJrKoLcu5cfKqGaZpUaAZqnjx456rYsso0N9DBXhgad2s+krDQ/tUq/OFz5NkXjsQqOnd+zbrWKmwpbHaWs7AtCdDXq4zEqjpf6WYKP1JCT63Z2UEbNAqvmyWIsxdY366rRpsxE7wDp0oSjkyw9t2UXCZLANnEkVklqcRk2DcjorJYQFPCcENDv/5w5dliHmVQ0iJ0274qRdaeLYWkZ8tfRVkVrJbBytQAAAAASUVORK5CYII=" />
							</view>
						</view>
						<view class="list-bt" @click="navi(item.id,item.stationId)">
							处理上报 →
						</view>
					</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	import statusBar from "../../components/status-bar/index.vue"
	import WatchItem from "../../components/watch-item/index.vue"
	import DateTime from "../../components/datetime/index.vue"
	import {$http} from "../common/util.js"
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
			},
			scrollH:'',
			pageIndex:1,
			pageRows:5,
			tableData: [],
			pageParam:{},
			timeStart:'',
			timeEnd:'',
			type:''
		}
		},
		computed: {},
		onLoad() {
			
			this.gethistory()
		},
		watch:{
			timeEnd(){
				this.gethistory()
			}
		},
		methods: {
			//左上角返回按钮
			onClickLeft() {
				uni.navigateBack();
			},
			navi(id,stationId){
				uni.navigateTo({
					url: "/pages/alarm/alarmreport/index?id=" + id+'&stationId='+stationId
				})
			},
			//获取历史报警
			gethistory(){
				var that = this
				$http({
					url: '/venus/mobilePhone/historyAlarm',
					data: {
						 pageIndex: that.pageIndex,
						 pageRows: that.pageRows*that.pageIndex,
						 timeStart:that.timeStart,
						 timeEnd:that.timeEnd,
						 type:that.type
					},
					success(res){
						console.log(res)
						that.tableData = res.data.tableData;
						
					}
				})
			},
			//到达底部触发
			reachBottom(){
				
				// console.log(1)
				 this.pageIndex++;
				// if(this.pageIndex)
				 this.gethistory();
			},
			//获取当前屏幕高度
			getHeight(){
				var that = this
				wx.getSystemInfo({
				          success: function(res) {
				            let scrollH = res.windowHeight;
				                that.scrollH = scrollH
				          }
				      });
			},
			starttime(e){
				console.log(e)
				this.timeStart = e
			},
			endtime(e){
				console.log(e)
				this.timeEnd = e
			},
			onChange(e){
				this.type = e.detail
			},
			onClick(){
				this.gethistory()
			}
		},
		mounted() {
			this.getHeight()
		},

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
				//padding-bottom: 15rpx;
				// position: absolute;
				// top: 30%;
				// width: 100%;
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
