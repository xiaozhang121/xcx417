<template>
	<view class="box">
		<!-- 切换导航-导航 -->
		<van-nav-bar title="监测站点" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
			<!-- <uni-ec-canvas
			   class="uni-ec-canvas"
			   id="uni-ec-canvas"
			   ref="uni-ec-canvas"
			   canvas-id="uni-ec-canvas"
			   :ec="ec"
			></uni-ec-canvas> --> 
			<!-- <van-tabs>
			  <van-tab title="站点详情" @click='show()'>
				<one v-if="active===0"></one>
			  </van-tab>
			  <van-tab title="历史记录">
				  <two v-if="active===1"></two> 
			  </van-tab>
			  <van-tab title="历史报警">
				  <three v-if="active===2"></three>
			  </van-tab>
			</van-tabs> -->
			<view class="tab">
				<view class="btn" v-for="(item,n) in title" @click="show(n)" :key='n'>
					<view class="btn-title" :class="n===index?'col':''">
						{{item}}
					</view>
				</view>
			</view>
			<one v-if="index===0" :receive='tableData'></one>
			<two v-if="index===1" :postid='id' ></two>
			<three v-if="index===2" :receive='tableData' :getmore='getmore'></three>
		</view>
	</view>
</template>

<script>
	import statusBar from "../../components/status-bar/index.vue"
	import WatchItem from "../../components/watch-item/index.vue"
	import one from "./one/index.vue"
	import two from "./two/index.vue"
	import three from "./three/index.vue" 
	import {$http} from "../common/util.js"
	
	export default {
		name: "user",
		components: {
			statusBar,
			WatchItem,
			one,
			two,
			three
		},
		data() {
		return {
			active: 0,
			arr:[0,1,2],
			index: 0,
			title: ['站点详情','历史记录','历史报警'],
			id:'',
			tableData:{},
			//date:'',
			getmore:0
		}
		},
		onReachBottom(){
			this.getmore++;//暴露给子组件 让子组件进行监听
		},
		computed: {},
		onLoad(option) {
			//console.log(option)
			this.id = option.id
			this.getDetail()
		},
		methods: {
			getChild(e){
				// console.log(e)
				//this.date = e
			},
			//左上角返回按钮
			onClickLeft() {
				uni.navigateBack()
			},
			onChange(){
				
			},
			getDetail(){
					var that = this
					$http({
						url: '/venus/crud/PnmStation/view',
						data: {
							 id:that.id
						},
						success(res){
						console.log(res)
						that.tableData = res.data;
						}
					})
			},
			show(n){
				this.index = n
			}
			

		},
		mounted() {
			// this.gettab();
			// this.gettol()
		},

	}
</script>

<style lang="less">
	.van-icon--image {
		width: 48rpx!important;
		height: 48rpx!important;
		margin-top: 20rpx;
		margin-right: 20rpx;
		float: right;
	}
	.box {
		height: 100%;
		background-color: #F3F3F3;
		.content {
			padding: 42px 0 0;
			
			.van-sticky{
				padding: 0 120rpx;
				.van-tabs__line {
					background-color: #005AC3;
				}
				.van-tab--active {
					color:#005AC3;
					// font-size: 32rpx;
					font-weight: 700;
				}
			}

		}
	}
	.tab {
		width: 100%;
		height: 80rpx;
		padding: 0 120rpx;
		display: flex;
		box-sizing: border-box;
		background-color: #FFFFFF;
	}
	.btn {
		padding: 0 20rpx;
		margin-top: 20rpx;
		// border: 1px solid #333;
		float: left;
		flex: 1;
		font-size: 28rpx;
		text-align: center;
		color: #999999;
		
		.btn-title{
			padding-bottom: 15rpx;
		}
	}
	.col{	
		color: #005AC3;
		border-bottom: 6rpx solid #005AC3;
	}
</style>
