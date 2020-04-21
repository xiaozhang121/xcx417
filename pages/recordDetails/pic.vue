<template>
	<view class="box">

		<!-- 切换导航-导航 -->
		<van-nav-bar title="查看图片" fixed left-arrow @click-left='onClickLeft' />
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
			<view class="img">
				<image :src="area" mode=""></image>
			</view>
			<view class="del">
				
			</view>
		</view>
	</view>
</template>

<script>
	import statusBar from "../../components/status-bar/index.vue"
	import WatchItem from "../../components/watch-item/index.vue"
	export default {
		name: "user",
		components: {
			statusBar,
			WatchItem
		},
		data() {
		return {
			area: ''
			}
		},
		computed: {},
		onLoad(option) {
			this.area = option.index
		},
		methods: {
			//左上角返回按钮
			onClickLeft() {
				uni.navigateBack()
			}
			
				// _previewImage(image) {
				// 			// this.imgArr = [];
				// 			this.imgArr.push(image);
				// 			//预览图片
				// 			uni.previewImage({
				// 				urls: this.imgArr,
				// 				current: this.imgArr[0]
				// 			});
				// 		}
		},
		mounted() {},

	}
</script>

<style lang="less">
	.box {
		// height: 100%;
		background-color: #333333;
		//padding: 30rpx 20rpx;
		height: 100%;
		overflow: hidden;
		.content {
			padding: 44px 0 0;
			box-sizing: border-box;
			.img {
				width: 622rpx;
				height: 382rpx;
				margin: 250rpx auto 0;
				image {
					width: 100%;
					height: 100%;
				}
			}
			.del {
				background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAAeCAYAAAA7MK6iAAADPklEQVRIS62Xy6tOURjGf0+R3HLL7bj+CSJGbknILSOKCSaKiQkDBs6UKNSZHyMpA+VSnOQUmUjOn3DcycBdinr07tb+2mdb+9ufk11f326vtd7nfd77Ej08thcB84EF6bcQ+JSOzgDeVX7vJb1uE6u2DbZ3AVOBb8B74G2ASPodZ21PqCgTik0Dvkq61U12I7Dt5cBeYEjSszYFq+u2VwGbgGuSXuTOZoFtb0umjYM//wW03Gt7SlL8raS7dRl/AdveD4xKejwewPoZ22uBRZKuVdfGACemX/4XaIX9OmCypHvltw5w8ukGSVf+B9MM80PA/dLnVeCTwOU2n9o+CJwBIvjiGQEuSRrspnDy+VFJ52NfAZxS5lUv0WvbwCxJRR7bngl8lNRLaka0L5B0W7YXA+skXc2YZxRYNk7TP5dUWqUjwvYB4EEArwT6mhI+GPbCppbHjWds7wZeBPB24IOkJzlmVWDbKwr/SCNN78n83YDXAHMC+DBwT9KrBuARSQWg7f4E3N/0nvYNS9rYIG8JsDmATwNny9qb8fMwsCeCqRfglJaDXYAnAicC+JikgaYAsh3A/ZKGbQeLjZJyjINluSf2ZxknixwbD/BxSXtq7OvK9QR8CjjXYuoq40LoeIFtd0zdFlw3gIt1M7YAF1ZpC662dIpILv0X0R1K5BgflDRajYMG4Ein2WUBibZ1s2FjAH+SdDEFRpFeNcbZlGuQ1ykgMU+tz5XMeu5Wi0MNuFMwqt8bgKPfD5dNYmfMUpKeZvI4fBV5HF2pKCIpnYp0Sb4vvqX16FI3JEVsjHlsrwbmSrpTbYsngAFJP2p1N7pPtL4ImL+E1faGkuGSFWX3KtdtxxB4RNKFQuHKwtIY0HJ9NdXlYBItsRxr64RCwZAXQRaK1tmOyZ766LMV+C7pUYN/QnhRtzNPBFhWKdvrgUmShspzuWFvH/BG0sMGgH/6nEDnSbpePdg03m6JyTDNxWN83itq8mnM5S+rTBsZ13weBx/kor2bAil6w7wxl2fbbS9z0g4gfPs13Y/KK8yvlD5Re+PqEvep+J+eZrA73ZRrBU7C+4B5FeEB8jkJjktbKFMoFPcrSfHe9fkDS1wqyl88drwAAAAASUVORK5CYII=);
				width: 60rpx;
				height: 60rpx;
				position: absolute;
				top: 70%;
				left: 50%;
				transform: translate(-50%,-50%);
			}
		}
	}
</style>
