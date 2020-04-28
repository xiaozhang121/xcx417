<template>
	<view class="box">

		<!-- 切换导航-导航 -->
		<van-nav-bar title="数据上报详情" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
			<!-- <van-cell-group>
			  <van-cell title="单元格" value="内容" />
			  <van-cell title="单元格" value="内容" label="描述信息" :border="false" />
			</van-cell-group> -->
			<view class="group">
					<van-cell-group><van-cell center title="站点名称" border= true :label="detail.id" size='large'/>
					
					<van-cell center title="采集地点"  :label="detail.reportSite"  size='large'/>
				
					<van-cell center title="上报类型"  :label="detail.reportType==1?'巡检上报':(item.reportType==2?'阀门开启度设置上报':'预警上报')" size='large'/>
					
					<van-cell center title="上报描述"  :label="detail.reportDescribe" size='large' />
					
				</van-cell-group>
			</view>
			<view class='group'>
				<van-cell-group >
					<van-cell center title="上报时间"  :label="detail.reportTime" size='large'/>
					
					<van-cell center title="上报人"  :label="detail.reportPerson" size='large'/>
				</van-cell-group>
			</view>
			<view class="group">
				<view class="pic-txt">
					现场图片
				</view>
				<view class='group-img'>
						<view class="img" v-for="item in imgURL" :key='item'>
								<image :src="item" mode=""  @click="_previewImage(item)"></image>
						</view>				    				
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
			imgArr: [],
			id:'',
			tableData:[],
			user:'',
			detail:{},
			imgURL:[]
			}
		},
		computed: {},
		onLoad(option) {
			console.log(option)
			this.id = option.id;
			this.getrecordDetails()
		},
		methods: {
			//左上角返回按钮
			onClickLeft() {
				uni.navigateBack()
			},
			watch(e){
				uni.navigateTo({
					url: '/pages/recordDetails/pic?index='+this.info
				})
			},
				_previewImage(image) {
							// this.imgArr = [];
							this.imgArr.push(image);
							//预览图片
							uni.previewImage({
								urls: this.imgArr,
								current: this.imgArr[0]
							});
						},
				getrecordDetails(){
					var that = this;
					var user = uni.getStorageSync('userinfo')
					this.user = user.id;
					$http({
						url: '/venus/crud/PnmHistoryReport/view',
						data: {
							 // pageIndex:that.pageIndex,
							 // pageRows:that.pageRows,
							 id: that.id
						},
						success(res){
							console.log(res)
							that.detail = res.data
							that.imgURL = res.data.imgUrl.split(',')
							//console.log(res.data.)
							// that.tableData = res.data.tableData
							
							// var tab = that.tableData.filter((item,index)=>{
								 
							// 	if(item.id*1===that.id.id*1){
									
							// 		return item
							// 	}
							// })
							// //that.detail = tab;
							// let [detail] = tab;
							// that.detail = detail;
							// console.log(that.detail)
						}
					})
				}
		},
		mounted() {},

	}
</script>

<style lang="less">
	.box {
		// height: 100%;
		background-color: #F3F3F3;
		//padding: 30rpx 20rpx;
		height: 100%;
		overflow: hidden;
		.content {
			padding: 44px 0 0;
			box-sizing: border-box;
			.group {
				background-color: #FFFFFF;
				margin-top: 20rpx;
				.van-cell__title,.van-cell__value {
					font-size: 28rpx;
				}
				.van-cell__label {
					font-size: 28rpx;
			}
			.pic-txt {
				padding: 30rpx 20rpx;
				font-size: 28rpx;
			}
			}
			.group-img {
				padding: 0 20rpx;
				white-space: nowrap;
				position: relative;
				display: flex;
				padding-bottom: 30rpx;
					.img {
						// flex: 1;
						width: 18%;
						height: 120rpx;
						// width: 120rpx;
						margin-right: 2%;
						float: left;
						image{
							width: 100%;
							height: 100%;
						}
					}
					.img:last-child {
						margin: 0;
					}

				
			}
		}
	}
</style>
