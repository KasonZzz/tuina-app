<template>
	<view class="container">
		<uni-nav-bar>

		</uni-nav-bar>
		<view class="content">
			<view class="member-card">
				<view class="info">
					<view class="title">
						<view class="wenyue-font" @tap="openBenefits">KasonZzz</view>

					</view>
					<image @tap="info" src="https://img2.woyaogexing.com/2021/01/28/1cb62cf83f2642b8bd427c3f58d3bc5b!400x400.webp"
					 class="avatar"></image>
					<view class="badage">
						Lv1
					</view>
				</view>
				<!-- <view class="row">
					<navigator class="grid" open-type="navigate" url="/pages/my/wallet">
						<image src="/static/images/my/me_icon_wallet.png"></image>
						<view class="title">技师招募</view>
					</navigator>
					<navigator class="grid" open-type="navigate" url="/pages/gifts/gifts">
						<image src="/static/images/my/me_icon_gift_card.png"></image>
						<view class="title">我是技师</view>
					</navigator>
				</view> -->
			</view>
		</view>

		<!-- <list-cell hover arrow>
			<view class="list-cell-wrapper">
				<view view="title">认证中心</view>
			</view>
		</list-cell> -->

		<list-cell hover arrow>
			<view class="list-cell-wrapper">
				<view view="title">帮助中心</view>
			</view>
		</list-cell>

		<list-cell hover arrow>
			<view class="list-cell-wrapper">
				<view view="title">服务协议</view>
			</view>
		</list-cell>


		<list-cell hover arrow>
			<view class="list-cell-wrapper">
				<view view="title">隐私政策</view>
			</view>
		</list-cell>

		<list-cell hover arrow>
			<view class="list-cell-wrapper">
				<view view="title">联系客服</view>
			</view>
		</list-cell>

		<list-cell hover arrow>
			<view class="list-cell-wrapper">
				<view view="title">系统反馈</view>
			</view>
		</list-cell>

		<list-cell hover arrow last>
			<view class="list-cell-wrapper">
				<view view="title">检查更新</view>
			</view>
		</list-cell>

		<list-cell hover arrow last>
			<view class="list-cell-wrapper">
				<view view="title">注销登陆</view>
			</view>
		</list-cell>


		<!-- 登录popup -->
		<login-popup ref="loginPopup"></login-popup>
	</view>
</template>

<script>
	import listCell from '@/components/list-cell/list-cell.vue'
	import loginPopup from './components/login-popup.vue'
	import {
		mapState
	} from 'vuex'

	export default {
		components: {
			listCell,
			loginPopup
		},
		data() {
			return {

			}
		},
		computed: {
			...mapState(['isLogin', 'userInfo'])
		},
		async onLoad() {

		},
		methods: {
			openLoginPopup() {
				if (this.isLogin) {
					return;
				} else {
					this.$refs['loginPopup'].open()
				}

			},
			info() {
				uni.navigateTo({
					url: '/pages/my/info'
				})
			},
			taskCenter() {
				uni.navigateTo({
					url: '/pages/task-center/task-center'
				})
			},
			openMember() {
				uni.navigateTo({
					url: '/pages/my/member'
				})
			},
			myCode() {
				uni.navigateTo({
					url: '/pages/my/code'
				})
			},
			openBenefits() {
				if (this.isLogin) {
					uni.navigateTo({
						url: '/pages/my/benefits'
					})
				} else {
					this.$refs['loginPopup'].open()
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	/* #ifdef H5 */
	page {
		height: auto;
		min-height: 100%;
	}

	/* #endif */

	.content {
		padding: 0 30rpx;
	}

	.welcome {
		position: relative;
		margin-top: -136rpx;
		display: flex;
		flex-direction: column;
		font-size: $font-size-lg;
		color: $text-color-warning;
	}

	.member-card {
		background-color: $bg-color-white;
		padding: 20rpx;
		display: flex;
		flex-direction: column;
		border-radius: $border-radius-base;
		margin-bottom: 40rpx;

		.info {
			position: relative;
			margin-top: -50rpx;
			display: flex;
			align-items: center;
			position: relative;
			padding: 20rpx 0;
			border-bottom: 1rpx solid rgba($color: $border-color, $alpha: 0.3);

			.title {
				flex: 1;
				font-size: 40rpx;
				color: $text-color-base;
				display: flex;
				align-items: center;

				.tips {
					margin-left: 10rpx;
					font-size: $font-size-sm;
					color: $text-color-assist;
					background-color: #e9e9e9;
					padding: 10rpx 30rpx;
					border-radius: 50rem !important;
					display: flex;
					align-items: center;

					image {
						width: 20rpx;
						height: 20rpx;
					}
				}
			}

			.avatar {
				width: 150rpx;
				height: 150rpx;
				border-radius: 100%;
			}

			.badage {
				font-family: 'neutra';
				position: absolute;
				bottom: 20rpx;
				left: 0;
				border: 2rpx solid $text-color-base;
				padding: 2rpx 20rpx;
				border-radius: $border-radius-lg;
				font-size: $font-size-base;
			}
		}

		.row {
			margin-top: $spacing-row-base;
			width: 100%;
			display: flex;
			align-items: center;

			.grid {
				flex: 1;
				flex-shrink: 0;
				display: flex;
				flex-direction: column;
				align-items: center;

				image {
					width: 100rpx;
					height: 100rpx;
				}

				.value {
					font-family: 'neutra';
					margin-bottom: $spacing-col-sm;
					font-size: $font-size-lg;
				}

				.title {
					font-size: $font-size-sm;
					color: $text-color-grey;
				}
			}
		}
	}

	.xinqiubobao {
		width: 100%;
		position: relative;

		.title {
			margin: 10rpx 0;
			font-size: $font-size-lg;
			font-weight: 500;
		}

		.swiper {
			height: 200rpx;
			margin-bottom: 10rpx;

			.swiper-item {

				.swiper-item-wrapper {
					display: flex;
					background-color: $bg-color-white;
					padding: 40rpx 60rpx;
					border-radius: $border-radius-base;
					align-items: center;
					margin-right: 40rpx;

					image {
						width: 100rpx;
						height: 100rpx;
						border-radius: 100%;
						margin-right: 20rpx;
					}

					.desc {
						display: flex;
						flex-direction: column;

						.title {
							font-size: $font-size-medium;
							font-weight: 500;
							margin-bottom: 10rpx;
						}

						.desc {
							font-size: $font-size-sm;
							color: $text-color-grey;
						}
					}
				}
			}
		}
	}

	.task-center {
		margin: 40rpx 0;
		background-color: $bg-color-white;
		padding: 10rpx 0;
		display: flex;
		align-items: center;
		border-radius: $border-radius-lg;

		.intro {
			flex: 1;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;

			.title {
				font-size: $font-size-lg;
				color: $text-color-base;
			}

			.subtitle {
				font-family: 'neutra';
				font-size: $font-size-sm;
			}
		}

		.image-wrapper {
			flex: 1;
			display: flex;
			justify-content: center;
			align-items: center;

			image {
				width: 200rpx;
				height: 200rpx;
			}
		}
	}

	.open-gift {
		width: 100%;
		background-color: $bg-color-white;
		padding: 30rpx 40rpx;
		margin-bottom: 20rpx;

		.header {
			display: flex;
			justify-content: space-between;
			align-items: center;
			margin-bottom: 20rpx;

			.title {
				font-size: $font-size-lg;
				font-weight: 500;
			}

			.subtitle {
				font-size: $font-size-base;
				color: $text-color-grey;
			}
		}

		.row {
			display: flex;
			flex-wrap: wrap;

			.grid {
				width: 33.3333%;
				display: flex;
				flex-direction: column;
				align-items: center;
				padding: 20rpx;

				image {
					width: 70rpx;
					height: 70rpx;
					margin-bottom: $spacing-row-base;
				}

				.title {
					font-size: $font-size-base;
					color: $text-color-base;
					display: flex;
					align-items: baseline;

					.number {
						margin-left: 5rpx;
						font-family: 'neutra';
						color: $color-warning;
					}
				}
			}
		}
	}

	.list-cell-wrapper {
		width: 100%;
		display: flex;
		justify-content: space-between;
		align-items: center;

		.title {
			font-size: $font-size-lg;
		}

		.subtitle {
			font-size: $font-size-sm;
			color: $text-color-assist;
		}
	}
</style>
