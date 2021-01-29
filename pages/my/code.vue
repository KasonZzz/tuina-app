<template>
	<view class="container">
		<view class="banner-swiper">
			<image  src="../../static/images/2.jpg" style="width: 100%" mode="aspectFill"></image>
		</view>

		<view class="main">
			<view class="userinfo">
				<image class="avatar" src="https://img2.woyaogexing.com/2021/01/28/1cb62cf83f2642b8bd427c3f58d3bc5b!400x400.webp"></image>
				<view class="username">KasonZzz</view>
				<view class="desc">该技师已完成健康认证</view>
			</view>
			<view style="text-align: center;">
				<image src="../../static/images/my/jkm.jpg" mode="widthFix"></image>
			</view>
		</view>
	</view>
</template>

<script>
	import uQRCode from '@/components/common/uqrcode'
	import uniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue'

	export default {
		components: {
			uniNavBar
		},
		data() {
			return {

			}
		},
		onShow() {
			let i = 1
			this.makeMemberCode(i)

			setInterval(() => {
				i++
				this.makeMemberCode(i)
			}, 30000)
		},
		methods: {
			back() {
				uni.navigateBack()
			},
			makeMemberCode(i) {
				uQRCode.make({
					canvasId: 'memberCode',
					componentInstance: this,
					text: `memberCode${i}`,
					size: uni.upx2px(350),
					margin: 20,
					backgroundColor: '#ffffff',
					foregroundColor: '#000000',
					fileType: 'jpg',
					correctLevel: uQRCode.defaults.correctLevel,
					success: res => {}
				})
			},
			//预览图片
			previewImage: function(e) {
				console.log(e);

			},
		}
	}
</script>

<style lang="scss" scoped>
	.container {
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		background-color: #FFFFFF;
	}


	page {
		max-height: 100%;
	}

	.banner-swiper {
		height: 25vh;
		/* #ifdef H5 */
		height: calc(25vh - 44px);
		/* #endif */

		image {
			height: 25vh;
		}
	}

	.content {
		width: 100%;
		padding: 0 30rpx;
		position: relative;
	}

	.bg {
		background-color: #424141;
		height: 25vh;
		/* #ifdef H5 */
		height: calc(25vh - 44px);
		/* #endif */
	}

	.main {
		flex: 1;
		display: flex;
		flex-direction: column;
	}

	.userinfo {
		display: flex;
		flex-direction: column;
		align-items: center;
		border-bottom: 1rpx solid rgba($color: $border-color, $alpha: 0.6);

		.avatar {
			position: relative;
			width: 140rpx;
			height: 140rpx;
			border-radius: 100%;
			margin-top: -70rpx;
			margin-bottom: 20rpx;
		}

		.username {
			font-size: $font-size-extra-lg;
			font-weight: bold;
			margin-bottom: 50rpx;
		}

		.desc {
			font-size: $font-size-sm;
			color: $text-color-assist;
			margin-bottom: 20rpx;
		}
	}

	.code-section {
		flex: 1;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		font-size: $font-size-base;
		color: $font-size-base;

		.tips {
			font-size: $font-size-sm;
			color: $text-color-assist;
		}
	}
</style>
