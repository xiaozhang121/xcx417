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
				<view class="user">
					<view class="photo">
						<image :src="avator" mode=""></image>
					</view>
					<view class="username">
						{{user}}
					</view>
					<view class="userid">
						{{phone}}
					</view>
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
						<navigator url="/pages/message/index">
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
						<navigator url="/pages/alarm/index">
							<image src="data:image/png;base64,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" mode=""></image>
						</navigator>
						<view class="text">
							预警
						</view>
					</view>
					<view class="navbox"  >
						<view class="fak">
							
						</view>
					</view>
					<view class="navbox"   >
						<view class="fak">
							
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import statusBar from "../../components/status-bar/index.vue"
	import {$http} from "../common/util.js"
	import uniEcCanvas from '../../uni-ec-canvas/uni-ec-canvas.vue'
	export default {
		name: "user",
		components: { 
			statusBar,
			 uniEcCanvas
			 },
		data() {
			return {
				// imgURL: this.$store.state.imgURL,
				user:'',
				avator:'',
				phone:'',
				userId:'',
				msg:''
			}
		},
		computed: {
			// MonitorVersion () {
			// 	return this.$store.state.MonitorVersion
			// }
		},
		onLoad() {
			this.login()
			this.getuser()
			this.getmessage()
		},
		methods: {
			//左上角返回按钮
	
		login(){
		let that = this; 				
		uni.login({				
					provider: 'weixin',				
					success: function(loginRes) {					
						console.log(loginRes);					
						// 获取用户信息					
						uni.getUserInfo({						
							provider: 'weixin',						
							success: function(res) {							
								console.log(res);							
									that.user = res.userInfo.nickName;
									//that.id = res.userInfo.id;	
									that.avator = res.userInfo.avatarUrl;					
								},
								});				
								},
								});
			},
		getuser(){
			var us = uni.getStorageSync('userinfo').phone
			this.phone = us.replace(/^(.{3})(.*)(.{4})$/, '$1 $2 $3')	
		},
		getmessage(){
			var that = this;
			var user = uni.getStorageSync('userinfo')
			that.userId = user.id;
			$http({
				url: '/venus/mobilePhone/messageUnread',
				data: {
					userId:that.userId
				},
				success(res){
					that.msg = res.msg
					console.log(that.msg)
				}
			})
			
		}
			
			
			
		},
		mounted() {}
	}
</script>

<style lang="less">
	.uni-ec-canvas {
		width: 100%;
		height: 100%;
		display: block;
		font-size: 12rpx;
	}
.box {
	background: #f5f7f9;
	height: 100%;
	overflow: hidden;
	.van-hairline--bottom:after{
		border-bottom: 0;
		}
	.van-nav-bar{
		background-image: linear-gradient(to right,#0068FF,#005AB4)!important;
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
				background-image: linear-gradient(to right,#0068FF,#005AB4)!important;
				position: relative;
				.user {
					position: absolute;
					top: 20%;
					left: 6%;
					height: 120rpx;
					width: 100%;
					color: #FFFFFF;
					.photo {
						width: 120rpx;
						height: 120rpx;
						border-radius: 50%;
						position: absolute;
						left: 0;
						top: 0;
						overflow: hidden;
						image {
							width: 100%;
							height: 100%;
						}
					}
					.username {
						position: absolute;
						left: 160rpx;
						top: 3%;
					}
					.userid {
						position: absolute;
						left: 160rpx;
						bottom: 3%;
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
				.fak {
					margin: 0 auto;
					width: 150rpx;
					height: 150rpx;
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
