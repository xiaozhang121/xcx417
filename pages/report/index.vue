<template>
	<view class="box">

		<!-- 切换导航-导航 -->
		<van-nav-bar title="数据采集上报" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
		<view class="content-top">
					<view class="select">
					<van-cell title="站点名称" is-link  :label="selectone" arrow-direction="down" @click='actone'/>
						<van-action-sheet
						  :show="showone"
						  :actions="actionone"
						  @close="onClose"
						  @select="onSelectone"
						/>
						<!-- <action-sheet :hidden="showone" bindchange="actionSheetChange">
						    <block v-for="item in 5">
						        <action-sheet-item >2</action-sheet-item>
						    </block>
						    <action-sheet-cancel >取消</action-sheet-cancel>
						</action-sheet> -->
					</view>
					
					<view class="write">
						<van-cell-group>
							<view class="van-text">
							采集地点
							</view>
						  <van-field
						    :value="value"
						    placeholder="请输入采集地点"
						    @change="onreportSite"
						  />
						 
						</van-cell-group>
					</view>
					<view class="select">
						<van-cell title="上报类型" is-link  :label='selecttwo' arrow-direction="down" @click='acttwo'/>
						<van-action-sheet
						  :show="showtwo"
						  :actions="actiontwo"
						  @close="onClose"
						  @select="onSelecttwo"
						/>
						
					</view>
					<view class="write">
						<van-cell-group>
							<view class="van-text">
							上报描述
							</view>
						  <van-field
						    :value="value"
						    placeholder="请输入用户名"
						    @change="onreportDescribe"
							:border='false'
						  />
						  
						</van-cell-group>
					</view>
		</view>
		<view class="content-bottom">
			<view class="bt-txt">
				上传现场图片
			</view>
			<van-uploader :file-list="fileList" :deletable='false' @after-read='afterRead'/>
		</view>
		<view class="report">
			<view class="report-one">
				<van-button type="default">取消</van-button>
			</view>
			<view class="report-one">
				<van-button color="linear-gradient(to right, #0068FF, #005AC3)" @click='report'>确认上报</van-button>
			</view>
		</view>
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
			WatchItem
		},
		data() {
		return {
			showone: false,
			showtwo: false,
			    actionone: [
			     
			    ],
				actiontwo: [
				],
				fileList: [],//上传图片
					userId:'',
					arr:[],
					warn:[],
					selectone:'请选择',
					selecttwo:'请选择',
					reportType:'',//上报类型
					stationId:'',//站点id
					reportPersonId:'',//上报人
					reportSite:'',//采集地点
					reportDescribe:''//站点描述
					
		}
		},
		mounted() {
			// this.gettype()
		},
		computed: {},
		onLoad(option) {
			//console.log(option)
			// console.log(option.stationId)
			// this.stationId = option.stationId
			// console.log(this.stationId)
			this.getdropdown();
			this.gettype()
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
			getdropdown(){
				var that = this;
				var user = uni.getStorageSync('userinfo')
				that.userId = user.id;
				$http({
					url: '/venus/select/custom',
					method:'POST',
					data: {
						entityName:"PnmStation",
						id:that.userId
					},
					success(res){
						for (var i=0;i<res.data.length;i++){
							that.actionone.push({name:res.data[i].label,value:res.data[i].value})
						}
					}
				})
			},
			gettype(){
				var that = this;
				$http({
					url: '/venus/select/dictionary',
					method:'POST',
					data:{entityName:"REPORT_TYPE"},
					success(res){
						for (var i=0;i<res.data.length;i++){
							that.actiontwo.push({name:res.data[i].label,value:res.data[i].value})
						}
						console.log(that.actiontwo)
					}
				})
			},
			onSelectone(e){
				this.selectone = e.detail.name
				//站点id
				this.stationId = e.detail.value
			},
			onSelecttwo(e){
				this.selecttwo = e.detail.name
				//上报类型id
				this.reportType = e.detail.value
			},
			report(){
				var that = this;
				var user = uni.getStorageSync('userinfo')
				that.reportPersonId = user.id;
				$http({
					url: '/venus/crud/PnmHistoryReport/add',
					method:'POST',
					data: {
						stationId:that.stationId,
						reportPersonId:that.reportPersonId,
						reportSite:that.reportSite,//采集地点
						reportDescribe:that.reportDescribe,//站点描述
						reportType:that.reportType,
						imgUrl:that.fileList
						
					},
					success(res){
						console.log(res)
						uni.showToast({
						  title: '数据采集上报成功'
						})
						 uni.navigateTo({
						 	url:'/pages/record/index'
						 })
					}
				})
			},
			onreportSite(e){
				this.reportSite = e.detail
			},
			onreportDescribe(e){
				this.reportDescribe = e.detail
			}
		} 
	}
</script>

<style lang="less">
	.box {
	height: 100%;
	background-color: #F3F3F3;
		.content {
			padding: 44px 0 0;
			box-sizing: border-box;
			.write {
				background-color: #FFFFFF;
				.van-text {
					font-size: 28rpx;
					padding: 10rpx 32rpx;
					background-color: #FFFFFF;
				}
				.van-cell {
					padding: 0 32rpx!important;
					padding-top: 6rpx;
					.van-cell__title {
					font-size: 28rpx;	
					}
				}
			}
			.select {
				background-color: #FFFFFF;
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
