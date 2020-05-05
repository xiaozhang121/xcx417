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
					<view class="van-text">
					站点名称
					</view>
				  <van-field
				    :value="value"
				    placeholder="请输入站点名"
				    @change="getreportPersonId"
				  />
			</view>
					<view class="write">
						
							<view class="van-text">
							采集地点
							</view>
						  <van-field
						    :value="value"
						    placeholder="请输入采集地点"
						    @change="getreportSite"
							
						  />
						
						
					</view>
					<view class="write mt">
					
							<view class="van-text">
							上述描述
							</view>
						  <van-field
						    :value="value"
						    placeholder="请输入上述描述"
						    @change="getreportDescribe"
						  />
						
					</view>
		</view>
		<view class="content-bottom">
			<view class="bt-txt">
				上传现场图片
			</view>
			<van-uploader :file-list="fileList"  @after-read='afterRead' @delete='del'/>
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
			    actionone: [
			      { name: '1' }
			    ],
				actiontwo: [
				  { name: '1' } 
				],
				fileList: [
		
				    ],
					reportPersonId:'',
					reportSite:'',
					reportDescribe:'',
					id:'',
					stationId:'',
					fina:[]//上传的图片地址
					
		}
		},
		computed: {},
		onLoad(option,stationId) {
			this.id = option.id
			this.stationId = option.stationId
			console.log(option)
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
			getreportPersonId(e){
				this.reportPersonId = e.detail
			},
			getreportSite(e){
				this.reportSite = e.detail
			},
			getreportDescribe(e){
				this.reportDescribe =e.detail
			},
			makesure(){
				var that = this;
				that.fileList.map((item,index)=>{
					that.fina.push(item.url)
				})
				that.fina = String(that.fina)
				console.log(that.fina)
				$http({
					method:'PUT',
					url: '/venus/crud/PnmAlarm/edit',
					data: {
						id: that.id,
						stationId:that.stationId,
						reportPersonId: that.reportPersonId,
						reportSite: that.reportSite,
						reportDescribe: that.reportDescribe,
						imgUrl: that.fina,
					},
					success(res){
						console.log(res)
						uni.showToast({
							title:'上报成功'
						})
						uni.navigateTo({
							url:"/pages/alarm/index"
						})
						// that.user = res.data.username;
						// that.id = res.data.id;	
						// console.log(res.tableData)
						//that.tableData = res.data.tableData;
						//uni.navigateBack()
					},
					fail(){
						uni.showToast({
							title:'预警上报失败',
							icon:'none'
						})
					}
				})
			},
			del(e){
				this.fileList.splice(e.detail.index,1)
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
				// .van-divider {
				// 	padding: 20rpx 30rpx 0!important;
				// 	margin: 0!important;
				// }
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
				.van-uploader__wrapper:nth-child(1){
					margin-right: 0!important;
				}
				.bt-txt{
					margin-bottom: 32rpx;
					font-size: 28rpx;
				}
				.van-uploader__preview{
					width: 120rpx;
					height: 120rpx;
					margin-right: 16rpx;
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
