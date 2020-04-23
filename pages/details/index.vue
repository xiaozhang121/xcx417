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
			  <van-tab title="站点详情" @click='active=0'>
				<one v-if="active===0"></one>
			  </van-tab>
			  <van-tab title="历史记录">
				  <two v-if="active===1" @click='active=1'></two> 
			  </van-tab>
			  <van-tab title="历史报警">
				  <three v-if="active===2"></three>
			  </van-tab>
			</van-tabs> -->
			<view class="btn" v-for="(item,n) in arr" @click="show(n)" >
			</view>
			<one v-if="index===0"></one>
			<two v-if="index===1"></two>
			<three v-if="index===2"></three>
		</view>
	</view>
</template>

<script>
	import statusBar from "../../components/status-bar/index.vue"
	import WatchItem from "../../components/watch-item/index.vue"
	import one from "./one/index.vue"
	import two from "./two/index.vue"
	import three from "./three/index.vue" 
	
	
	export default {
		name: "user",
		components: {
			statusBar,
			WatchItem,
			one,
			two,
			three,
			
		},
		data() {
		return {
			active: 0,
			arr:[0,1,2],
			index: 0
		}
		},
		computed: {},
		onLoad(option) {
			console.log(option)
			this.id = option.id
		},
		methods: {
			//左上角返回按钮
			onClickLeft() {
				uni.navigateBack()
			},
			onChange(){
				
			},
			getDetail(){
				
			},
			show(n){
				this.index = n
				
			}

		},
		mounted() {},

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
	.btn {
		width: 20px;
		height: 20px;
		border: 1px solid #333;
		
	}
</style>
