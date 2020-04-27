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
					<van-cell title="站点名称" is-link value="内容" label='请选择' arrow-direction="down" @click='actone'/>
						<van-action-sheet
						  :show="showone"
						  :actions="actionone"
						  @close="onClose"
						  @select="onSelect"
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
						    placeholder="请输入用户名"
						    @change="onChange"
							:border='false'
						  />
						 
						</van-cell-group>
					</view>
					<view class="select">
						<van-cell title="上报类型" is-link value="内容" label='请选择' arrow-direction="down" @click='acttwo'/>
						<van-action-sheet
						  :show="showtwo"
						  :actions="actiontwo"
						  @close="onClose"
						  @select="onSelect"
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
						    @change="onChange"
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
				<van-button type="default">默认按钮</van-button>
			</view>
			<view class="report-one">
				<van-button color="linear-gradient(to right, #0068FF, #005AC3)">渐变色按钮</van-button>
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
			      { name: '1'},
				   { name: '12'},
				    { name: '12'}
			    ],
				actiontwo: [
				  // { name: '1' } 
				],
				fileList: [
				     
				    ],
					stationId:'',
					userId:'',
					arr:[]
		}
		},
		mounted() {
			this.gettype()
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
						console.log(res)
						//this.arr.push()
						res.data.map((item,index)=>{
							//console.log(item)
							that.arr.push(item.stationName)
						})
						var fo = that.arr.forEach((item,index)=>{
							return [{name:item}]
						})
						console.log(fo)
					
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
						console.log(res.data)
					
					}
				})
			},
			onSelect(e){
				console.log(e.detail.name)
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
