<template>
	<view class="one">
		<view class="swi">
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item>
					<view class="swiper-item"></view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item"></view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item"></view>
				</swiper-item>
			</swiper>
		</view>
		<view class="form">
			<view class="">
				<van-cell-group>
				<van-cell title='南京六合站' size="large"></van-cell>
				  <van-cell title="负责人:" value="内容" />
				  <van-cell title="手机号:" value="内容" />
				  <van-cell title="地理位置:" value="内容" />
				</van-cell-group>
			</view>
			<view class="mid">
				<van-cell-group>
				  <van-cell title="负责人:" value="内容" />
				  <van-cell title="手机号:" value="内容" />
				  <van-cell title="地理位置:" value="内容" />
				</van-cell-group>
			</view>
			<view class="mid">
				<van-cell-group>
				  <van-cell title="负责人:" value="内容" />
				  <van-cell title="手机号:" value="内容" />
				  <van-cell title="地理位置:" value="内容" />
				</van-cell-group>
			</view>
			<view class="bm">
				<van-cell-group>
				  <van-cell title="负责人:" value="内容" />
				  <van-cell title="手机号:" value="内容" />
				</van-cell-group>
			</view>
			
		</view>
	</view>
</template>

<script>
</script>

<style lang="less">
	swiper {
		width: 100%;
		height: 420rpx;
		.swiper-item {
			width: 100%;
			height: 100%;
			background-color: yellow;
		}
	}
	.form {
		background-color: rgb(243, 243, 243);
		padding: 0 0 20rpx 0;
	}
	.mid {
		margin: 20rpx 0;
	}
</style>
