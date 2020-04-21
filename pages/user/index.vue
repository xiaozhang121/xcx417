<template>
	<view class="box">
		
		<!-- 切换导航-导航 -->
		<van-nav-bar
			title="智能管网"
			fixed
		/>
		<!-- 导航站位 -->
		<status-bar />
		<!-- 内容展示 -->
		<view class="content">
			<!-- <van-skeleton title row="3" :loading="!MonitorVersion" >
				<image class="logo" :src="imgURL + '/user.png'" mode="widthFix"></image>
				<view class="shopBox">
					<van-button size="mini" custom-style="padding: 12px;height: auto;font-size: 32px;border:none;border-radius: 50%;" color="#08CFC0" type="default">
						<van-icon name="shopping-cart-o" />
					</van-button>
				</view>
			</van-skeleton> -->
			<view class="userinfo">
				<view class="photo">
					<image src="data:image/png;base64,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" mode=""></image>
				</view>
			</view>
			<view class="bd">
				<view class="navs">
					<view class="navbox">
						<navigator url="/pages/watch/index">
							<image src="data:image/png;base64,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" mode=""></image>
						</navigator>
						<view class="text">
							检测站点
						</view>
					</view>
					<view class="navbox">
						<navigator url="/pages/login/index">
						<image src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAFAAAABQCAYAAACOEfKtAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAVqSURBVHhe7Z1PT5xFHMe/M8+zYENJWlOEUkFpjDGxN3kB5WYUeiT26EHrC/DuG+AFSC+e1MSrjUnjAb31gJ701kBLQwsFrZT/u8/MOL/nmQV22WWfZ5/ZfQZ2PgnZ+Q0bGD6ZP7+ZBwaGdllYCLF7cxD8cEBH/QhLfSjr1xIPkjc4SkUK9OEQjB+icliG7N/F3vhrzDJh3pGJbALnF0uYGBpCpK4gYJdM7cWgIvfQx7ewvLGBe5MVU9uSdAJJ3NjwMBANIeDc1F5MhJRAuIFn6+tpRJ4tsJfE1VMVeenxGqamIlN7iuZSlGK4fvU6Ajncc/II+pnpZ98eH41dNKHxJ35SAQaX3wMPLpua3kaKHWxPPG600DToWdq2l1cLuSAn5KaO0wJ/XRrz8hpATshNHbUCF1avQYZDJvLUQ27I0QmOBS6oEPvlU4Y9dZAjyk4MxwKjpdGeXG2zQo7i1C4hEfaX6kMU1HRNz1novNj0wkTgsyej4CzdrsST9MKbOkfWmCHL6UDAk4UoHKQXhu+W38Ao/zCu9GTjufybYwhXTOjJinbHUbpgx1LdRLvjiMRRTuPJiHbH45NkV2HsfYho1ETuwUMtUDjaA0meEj+A8+/BZbziOYeQWqCLuw+SJ8V8UsYghJp3UmKJB+7KI3FV4qHspkS3BJIgKeZq5FUhiZGaM5EzuCOQ5FEvY2i+aHD2EZT8xkRO4IbAI3m6l7WCYcYliW4IpKGZRl6VROKXJiqU4gVSb6KhmRUGLVDOmKgwihVI8qg3tY8eysVKLE4gDcF88qrQfJi9B1uiIIG618RD0BJKZptDLVKAwHjI2V1FKW+Mk+/uS+y2QBpqnUlBqhK7fPjQXYFK3DOlzkASOZ82UVdgePi0exMw9Y4gjB/GNEWp22DqronqeQCF56bcGCkf6O9x9nss0l2BqZGLplALxxQk3zaRExSXxrSDY/KI8yXQQbzAnHiBOfECc+IF5sQLzEln8kBKmDn/Vn/1dNsqhftg/L6JNE3yQPBJU9CIOd382yY4G0q+pfyqEwl2Z3ogbafSyotRJ8SkJaU8gtrSoS2efYHJo8dmW7EiuduJx6L2BUrovWyDx5JFE5/W6LZZxr5AhS9MqX0U+xFK/VnzQQcJebHRtjosLyJtHpaSIBZkPKFuttC0QOFrvWD9ZqLc2O2BUrU5UbORTPNTnpNn1fSorC1s9kD9dWTyC0HOw+lg94+knA+LPbD4Z7TpsddWOwKT5xBdPUrPybStZyd2BPLAxbzvbCy1Ob/AePJvd/EoEt1mC4l1foFC0UNy9xLnVlCbqe05sTCE2WemcA7J3/b8AjMdGjiGhbbbWUR6mPwCJX43pfOHhbY7+mD9/MDju6Q87aHd0R/apL4nylOHdschIy+wXbQ7jjDwAttFu9NzoNo3oScr2h3HBv4zoScr2h3H5xMHOh86MFWetJAz7S5JpBXfil896YlYPHITgTtbL5MLBz2pIFeXx9apmAicvVWGCF7GZU9ryNUUi2+1PN4L7z9a87uSFJCj6bEXJjohcHZWINxdMZGnKfwpGDua7o4FEh/f+hdltmYiTz3kZvqdVyaKqRVIzIyvggfO/TZ84Si2Fbup47RAIryxhKhSNpGHXLx+tGyiGppfeUdX//68NIb+Hr8StCI28enEip73lKmpofWdgXRn6EFlvOfuF5RKoXKwgjsfbJqahqST8ovsh3wygn72JuQFvyaUxAn5D/i7a/iEH5rapmTrVYuqhM3VEcjKNSdvPMpFICDUJt56ex2TzPI/I2jEwxcDENFVsMpA/C8wyiLUa1LgvNh4y6qTYUabhiBCKdzBXvAKd27smXdkAPgfNWu+4Yrr2cUAAAAASUVORK5CYII=" mode=""></image>
						</navigator>
						<view class="text">
							消息通知
						</view>
					</view>
					<view class="navbox">
						<navigator url="/pages/record/index">
							<image src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAFAAAABQCAYAAACOEfKtAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAATbSURBVHhe7ZzNbxtFFMDfzHrXjlMngEQPBUscEEj4wKUSCumhHCoQB6iEmjMHJK7Q/gEhf0AlrlXhyiEIiRMgtRIcCgipEheMBKo4ULiA1AYcxx/7Mby3fsa14zhe73g9a89Pcjxv5Cian2d25s1uRsCs7O5KuPiMB2sFD3zpgGoXIKw44AaSP2EmfiECpxGCKAXgRiG0gi5cfLsDQij+RCKSCVQo7dvqOkSVEsjQ5drloKS60G51YPt+E8RexLWnMp1AEvfDs2egA+vgOLP32jwQhgqK0ISX7h1OI3KyjFUSN0pf5Jcocu9kkZOvV7drFQicMysnj6A2U9svoIMJjBcTTxDPPQGu8LhmtfHx+vjNrw/G9cTxPdDKG4ZcvP7i4xwNcVzgrf1NK28MfrsYuxlhWODdG2VYC9Y5soxCbsjRIwwE0nWvWT5m2DICOaLVCTMQSLPNKs62SSFHtLRjegL39x3wOkNd0zIBWhdzL+wJfLJpe18SyBWtkZGewK5jZ92kRDgrIwK+3i2A+/zZuNKSDP+Xv7AH1kocWhJTK0ko+Mu1LZUl6E6CZ/gGqMmgOwmBcDi0JOVAOFZgGrwS9kC7/psdl4awJRVWYEoE3PnkHJf14QRV8NWr+P1scI0hqDpesr4HJf7litToFxiFV0GoaxyZh0KJwn0fW17nmlToHcIq3DFaHiFEDXOwjzlKjWaB0TtcMhxRxZHyMgep0Csw/nZXCzsLp8QKTIkVmBIrMCVWYEr0LqRV8CeXxhOpBkjxE0dzRG1i017gYDxKXAHpfMfRzGQnUMEHIAs3OZo/Qm1AFHx2okhNAjMawurnTOURcb4rr3M0NzISKP7hQrYo0LZpcBJZTSJbcZ6cJTSEIbzK0dzIdhIBdR+U+oOD+SLkFpfGk7tJxDTyNYksL1ZgSqzAlFiBKcl3JhJ2PwQpr3CUDJuJII73HpcWRkYCF5SJZEBW10DKRF7jsj7oFuqCyXYhTfdkQenJT4V4Gn9UOUqOzURSYjMRM7ACU2IFpsQKTIkVmBK9ArPaLNWBcLQs7vUKFGqfS4aDqaWRzwcK7zpE0accmUk8SlxtObTehXQfevZOhJi+yRr+hfGP+SpV7WUTU6DlhjxlQbIOUn6Fi2iDH/GdFtW9hg06PZeN5blv6RpyupHxWVKmYrg8cieh2zZToOnyCHQn4TEVcmgOeZBHoDvsgYYN4bzII9CdhMD1OVw8eZJHoDtcB9bbHGaLksNLibzJi6m3JbyyF0AzCLgmO+KbTOqjXkA3nXImj5yhu14msikW0wuFuwui8BS+X8pXz0PWN1r01hP4e7EZHzhomQ5ydevHJhUH/2x95/MKwBG+LKdTbsCFyw0qDTYTtt88NDorMQVytH35kKNHBNIxwEW1tDfA9dE8wHH7/+Xu+HkJdihPYDB0+wx6YB/6gOt3OLL0kU57VB5xXCDxxW8PQRSzXxuaShtC2Np5yNEQk488oTNDV/1I0FKhCed3TpwbxvfAPpfwF0uNg5VcI1KbH2DbJ8gjJgskzr97BNG9v+NvYhVEUhv9Tq/Nb2DbTyHZqUV07OXtcxXwyuWlO/HIxfWdQnFTnqHfZ3YJd2+4EJTXoCU9cAoCXNpbxJfpYqmHeU4EPr7CQEEr6sLZoxaOtBm29QD+A9ziyZXSziMIAAAAAElFTkSuQmCC" mode=""></image>
						</navigator>
						<view class="text">
							数据采集上报
						</view>
					</view>
				</view>
				<view class="navs">
					<view class="navbox" >
						<navigator url="">
							<image src="data:image/png;base64,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" mode=""></image>
						</navigator>
						<view class="text">
							预警
						</view>
					</view>
					<view class="navbox"  >
						<navigator url=""></navigator>
						
					</view>
					<view class="navbox"   >
						<navigator url=""></navigator>
						
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import statusBar from "../../components/status-bar/index.vue"
	export default {
		name: "user",
		components: { statusBar },
		data() {
			return {
				imgURL: this.$store.state.imgURL
			}
		},
		computed: {
			// MonitorVersion () {
			// 	return this.$store.state.MonitorVersion
			// }
		},
		onLoad() {},
		methods: {
			//左上角返回按钮
		onClickLeft(){
			}
		},
		mounted() {}
	}
</script>

<style lang="less">
.box {
	background: #f5f7f9;
	height: 100%;
	overflow: hidden;
	.van-hairline--bottom:after{
		border-bottom: 0;
		}
	.van-nav-bar{
		background-color: rgb(0, 95, 207)!important;
		.van-nav-bar__title{
			font-size: 28rpx;
			color: white;
			}
	}
	.content {
		padding: 42px 0 18px;
		height: 100vh;
		box-sizing: border-box;
		background: #f5f7f9;
			.userinfo {
				height: 30%;
				border-bottom: 1px solid #333;
				background-color: rgb(0, 95, 207)!important;
				position: relative;
				.photo {
					width: 120rpx;
					height: 120rpx;
					border-radius: 50%;
					position: absolute;
					top: 42%;
					left: 40rpx;
					transform: translate(0,-50%);
					overflow: hidden;
					image {
						width: 100%;
						height: 100%;
					}
				}
	}
	.bd {
		height: 100%;
		width: 100%;
		border-radius: 50rpx 50rpx 0 0;
		border: 1px solid white;
		position: relative;
		top: -8%;
		background-color: white;
		padding: 10% 0 0 0 ;
		.navs {
			display: flex;
			 flex-wrap:wrap;
			justify-content: space-around;
			align-items: center;
			margin-bottom: 50rpx;
			.navbox {
				navigator {
					display: block;
					margin: 0 auto;
					width: 150rpx;
					height: 150rpx;
					image {
						width: 100%;
						height: 100%;
					}
				}
				.text {
					font-size: 32rpx;
					text-align: center;
					margin-top: 20rpx;
					color: #333;
				}
			}
		}
		.navs-low {
			display: flex;
			 flex-wrap:wrap;
			 justify-content: space-between;
			 align-items: center;
			margin-bottom: 50rpx;
			.navbox {
				navigator {
					width: 150rpx;
					height: 150rpx;
					border: 1px solid #333;
					image {
						width: 100%;
						height: 100%;
					}
				}
				.text {
					font-size: 32rpx;
					text-align: center;
				}
			}
		}
	}
}
}
 

// .logo {
// 	width: 100%;
// }
// .shopBox {
// 	text-align: right;
// 	padding: 20rpx;
// 	box-sizing: border-box;
// }
</style>
