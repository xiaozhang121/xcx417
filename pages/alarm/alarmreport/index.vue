<template>
	<view class="box">

		<!-- 切换导航-导航 -->
		<van-nav-bar title="预警处理上报" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
		<view class="content-top">
			<!-- <view class="">
				<van-cell-group>
				  <van-field
				    :value="value"
				    placeholder="请输入用户名"
				    border=true
				    @change="onChange"
				  />
				  <van-field
				    :value="value"
				    placeholder="请输入用户名"
				    :border="false"
				    @change="onChange"
				  />
				  <van-field
				    :value="value"
				    placeholder="请输入用户名"
				    :border="false"
				    @change="onChange"
				  />
				</van-cell-group>
			</view> -->
			<view class="write">
				<van-cell-group>
					<view class="van-text">
					采集地点
					</view>
				  <van-field
					:border = 'true'
				    :value="value"
				    placeholder="请输入用户名"
				    @change="onChange"
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
						    @change="onChange"
							
						  />
						</van-cell-group>
						<van-divider />
					</view>
					<view class="write mt">
						<van-cell-group>
							<view class="van-text">
							采集地点
							</view>
						  <van-field
						    :value="value"
						    placeholder="请输入用户名"
						    @change="onChange"
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
				<van-button color="linear-gradient(to right, #0068FF, #005AC3)">确认上报</van-button>
			</view>
		</view>
			</view>
	</view>
</template>

<script>
	import statusBar from "../../../components/status-bar/index.vue"
	import WatchItem from "../../../components/watch-item/index.vue"
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
				      { url: 'https://img.yzcdn.cn/vant/leaf.jpg', name: '图片1' },
				      {
				        url: 'http://iph.href.lu/60x60?text=default',
				        name: '图片2',
				        isImage: true
				      }
				    ]
		}
		},
		computed: {},
		onLoad() {},
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
				const { file } = event.detail;
				console.log(file)
				 uni.uploadFile({
				      url: 'https://example.weixin.qq.com/upload', // 仅为示例，非真实的接口地址
				      filePath: file.path,
				      name: 'file',
				      formData: { user: 'test' },
				      success(res) {
				        // 上传完成需要更新 fileList
						console,log(1)
						this.fileList.push({ ...file, url: res.data })
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
