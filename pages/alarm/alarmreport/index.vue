<template>
	<view class="box">

		<!-- 切换导航-导航 -->
		<van-nav-bar title="预警处理上报" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
		<view class="content-top">
			<view class="write">
				<van-cell-group>
					<view class="van-text">
					站点名称
					</view>
				  <van-field
					:border = 'true'
				    :value="value"
				    placeholder="请输入用户名"
				    @change="getstationId"
				  />
				</van-cell-group>
				<van-divider />
			</view>
					<view class="write">
						<van-cell-group>
							<view class="van-text">
							采集地点
							</view>
						  <van-field
						    :value="value"
						    placeholder="请输入用户名"
						    @change="getreportSite"
							
						  />
						</van-cell-group>
						<van-divider />
					</view>
					<view class="write mt">
						<van-cell-group>
							<view class="van-text">
							上述描述
							</view>
						  <van-field
						    :value="value"
						    placeholder="请输入用户名"
						    @change="getreportDescribe"
						  />
						</van-cell-group>
					</view>
		</view>
		<view class="content-bottom">
			<view class="bt-txt">
				上传现场图片
			</view>
			<van-uploader :file-list="fileList"  @after-read='afterRead'/>
		</view>
		<view class="report">
			<view class="report-one">
				<van-button type="default">取消</van-button>
			</view>
			<view class="report-one">
				<van-button color="linear-gradient(to right, #0068FF, #005AC3)" @click = 'makesure'>确认上报</van-button>
			</view>
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
			showone: false,
			showtwo: false,
			reportSite: '',
			    actionone: [
			      { name: '1' }
			    ],
				actiontwo: [
				  { name: '1' } 
				],
				fileList: [
		
				    ],
					stationId:'',
					reportSite:'',
					reportDescribe:'',
					id:''
					
		}
		},
		computed: {},
		onLoad(option) {
			console.log(option)
			this.id = option
		},
		methods: {
			//左上角返回按钮
			onClickLeft() {
				uni.navigateBack()
			},
			nav(){
				   uni.navigateTo({
				            url:"/pages/report/index"
				        })
			},
			 onClose() {
			    this.showone = false;
				this.showtwo = false;
			  },
			  actone(){
				  this.showone = true
			  },
			  acttwo(){
					this.showtwo = true
			  },
			  onGetUserInfo(e) {
			    console.log(e.detail)
			  },
			afterRead(event){
				this.fileList.push({url: event.detail.file.path })
					
			},
			getstationId(e){
				this.stationId = e.detail
			},
			getreportSite(e){
				this.reportSite = e.detail
			},
			getreportDescribe(e){
				this.reportDescribe =e.detail
			},
			makesure(){
				var that = this
				$http({
					url: 'https://nei.netease.com/api/apimock-v2/e64ee4e782c695855b9f3645456ae8ce/venus/mobilePhone/historyAlarm?stationId=&type=&userId=&timeStart=&timeEnd=&pageIndex=&pageRows=',
					data: {
						id: that.id,
						stationId: that.stationId,
						reportSite: that.reportSite,
						reportDescribe: that.reportDescribe,
						imgUrl: that.fileList,
						repostPersonId:22
						
					},
					success(res){
						console.log(res)
						// that.user = res.data.username;
						// that.id = res.data.id;	
						// console.log(res.tableData)
						that.tableData = res.data.tableData;
						uni.navigateBack()
					}
				})
			}
			
		}
	}
</script>

<style lang="less">
	.mt {
		padding-bottom: 20rpx!important;
	}
	.box {
	height: 100%;
	background-color: #F3F3F3;
		.content {
			padding: 44px 0 0;
			box-sizing: border-box;
			.write {
				padding: 30rpx 0 0;
				background-color: #FFFFFF;
				// border-bottom: 1px solid #333;
				.van-divider {
					padding: 20rpx 30rpx 0!important;
					margin: 0!important;
				}
				.van-text {
					font-size: 28rpx;
					padding: 0 32rpx;
					background-color: #FFFFFF;
				}
				.van-cell {
					padding: 0 32rpx!important;
					padding-top: 6rpx;
					
				}
			}
			.content-top {
				margin-top: 20rpx;
			}
			.content-bottom {
				margin-top: 20rpx;
				background-color: #FFFFFF;
				padding: 30rpx 32rpx;
				.bt-txt{
					margin-bottom: 32rpx;
					font-size: 28rpx;
				}
				.van-uploader__preview{
					width: 124rpx;
					height: 124rpx;
					image {
						width: 100%!important;
						height: 100%!important;
					}
				}
				.van-uploader__upload{
					width: 124rpx!important;
					height: 124rpx!important;
				}
			}
			.report {
				display: flex;
				position: fixed;
				width: 100%;
				bottom: 0;
				.report-one {
					flex: 1;
					width: 100%;
					.van-button--normal {
						width: 100%;
					}
				}
			}
		}
	}
</style>
