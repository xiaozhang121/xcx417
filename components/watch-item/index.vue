<template>
	<view class="">
		<view class="list" v-for="item in receive" :key='item' @click="enter(item.id)">
			<view class="list-title">
				<view class="title-tp">
					<text class="name">{{item.stationName}}</text>
					<navigator class="normal" url="/pages/details/index">{{item.workStatus==1?'在线':'离线'}}</navigator>
					<view class="ico">
						<van-icon name="arrow"/>
					</view>
				</view>
				<view class="title-bd">
					编号： {{item.stationCode}}
				</view>
			</view>
			<view class="list-main">
				<view class="main-tp">
					<text>流量: {{item.waterFlow}}</text>
					<text>压力: {{item.waterPressure}}</text>
				</view>
				<view class="main-bd">
					位置: {{item.address}}
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:["receive"],
		methods:{
			enter(id){
				uni.navigateTo({
					url:'/pages/details/index?id='+id
				})
			}
		}
	}
</script>

<style lang="less">
	
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
				margin-bottom: 15rpx;
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
					color: #00C3A2FF;
				}
			}
			.title-bd {
				color: #666666FF;
				margin-bottom: 30rpx;
			}
		}
		.list-main {
			margin: 15rpx 0;
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
</style>
