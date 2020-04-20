<template>
	<view class="list">
		<view class="list-title">
			<view class="title-tp">
				<text class="name">南京六合站</text>
				<navigator class="normal" url="/pages/details/index">正常</navigator>
				<view class="ico">
					<van-icon name="arrow"/>
				</view>
			</view>
			<view class="title-bd">
				编号： 00121530
			</view>
		</view>
		<view class="list-main">
			<view class="main-tp">
				<text>流量: 735^3/h</text>
				<text>压力: 5kPa</text>
			</view>
			<view class="main-bd">
				位置: 南京市六合区宁六路219号
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
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
