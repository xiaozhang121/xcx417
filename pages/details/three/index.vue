<template>
	<view class="">
		<view class="choose">
			<view class="choose-time" v-for="(item,index) in choose" @click="sele(index)" :class="currentindex===index?'select':''" :key='index'>
				{{item}}
			</view>
		</view>
		<view class="card">
			<view class="list" v-for="(item,index) in 5" :key='index'>
				<view class="list-title">
					<view class="title-tp">
						<text class="name">2020.03.29 12:11:42</text>
						<text class="normal">爆管</text>
					</view>
				</view>
				<view class="list-main">
					<view class="main-tp">
						<text>流量: 735^3/h</text>
						<text>压力: 5kPa</text>
					</view>
					<view class="main-tp">
						<text>流量: 735^3/h</text>
						<text>压力: 5kPa</text>
					</view>
					<view class="main-bd">
						位置: 南京市六合区宁六路219号
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return {
			choose: ['全部','爆管','泄露','无信号'],
			currentindex:0
			}
		},
			methods: {
			sele(e){
				this.currentindex = e
			}
		
			
		},
	}
</script>

<style lang="less">
	.uni-ec-canvas {
		width: 100%;
		height: 100%;
		display: block;
	}
	.choose {
		padding: 36rpx 100rpx;
		background-color: rgb(243, 243, 243);
		display: flex;
		.choose-time {
			font-size: 28rpx;
			height: 56rpx;
			background-color: #CCCCCC;
			flex: 1;
			text-align: center;
			margin-right: 20rpx;
			line-height: 56rpx;
			border-radius: 30rpx;
			color: #FFFFFF;
			}
			.select {
				background-color: #005AC3;
			}
			view:nth-child(5) {
					margin-right: 0;
		}
	}
	.card {
		background-color: rgb(243, 243, 243);
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
					margin-bottom: 30rpx;
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
					color: #666666FF;
					margin-bottom: 30rpx;
				}
			}
			.list-main {
				margin: 20rpx 0;
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
	}
</style>
