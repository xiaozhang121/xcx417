<template>
	<view class="one">
		<view class="swi">
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item>
					<view class="swiper-item">
						<image :src="receive.avator" mode=""></image>
					</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item">
						<image :src="receive.avator" mode=""></image>
					</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item">
						<image :src="receive.avator" mode=""></image>
					</view>
				</swiper-item>
			</swiper>
		</view>
		<view class="form">
			<view class="">
				<van-cell-group>
				<van-cell :title='recieve.address' size="large"></van-cell>
				  <van-cell title="负责人:" :value="receive.id" />
				  <van-cell title="手机号:" :value="receive.phone" />
				  <van-cell title="地理位置:" :value="receive.address" />
				</van-cell-group>
			</view>
			<view class="mid">
				<van-cell-group>
				  <van-cell title="站点管材类型:" :value="recieve.pipeMaterial" />
				  <van-cell title="所属管网:" :value="receive.mainCanal" />
				  <van-cell title="上游管点:" :value="receive.upstreamPoint" />
				  <van-cell title="下游管点:" :value="receive.downstreamPoint" />
				</van-cell-group>
			</view>
			<view class="mid">
				<van-cell-group>
				  <van-cell title="阀门类型:" :value="receive.valveType" />
				  <van-cell title="阀门型号:" :value="receive.valveCode" />
				  <van-cell title="阀门安装日期:" :value="receive.valveInstallTime" />
				  <van-cell title="阀门开启度:" :value="receive.openStatus" />
				</van-cell-group>
			</view>
			<view class="bm">
				<van-cell-group>
				  <van-cell title="流量:" :value="recieve.waterFlow" />
				  <van-cell title="压力:" :value="receive.waterPressure" />
				   <van-cell title="工作状态:" :value="receive.alarmStatus===1?'正常':''" />
				</van-cell-group>
			</view>
			
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return {
				
			}
		},
		props:["receive"]
	}
</script>

<style lang="less">
	swiper {
		width: 100%;
		height: 420rpx;
		.swiper-item {
			width: 100%;
			height: 100%;
			image{
				width: 100%;
				height: 100%;
			}
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
