<template>
	<view class="container">
		<!-- 首页导航栏 -->
		<swiper class="banner-swiper" circular autoplay :interval="5000" :duration="1000">
			<swiper-item class="banner-swiper-item" v-for="(item, index) in swipers" :key="index">
				<image :src="item" mode="widthFix"></image>
			</swiper-item>
		</swiper>
		<view class="content">
			<!-- 中间按钮 -->
			<view class="section-1">
				<view class="item" @click="jump('/pages/entertain/entertain')">
					<image src="/static/images/home/nav-001.png" mode="widthFix"></image>
					<view class="wenyue-font">寻找项目</view>
					<view class="text-color-assist">下单免排队</view>
				</view>
				<view class="item" @click="jump('/pages/massagist/massagist')">
					<image src="/static/images/home/nav-002.png" mode="widthFix"></image>
					<view class="wenyue-font">寻找技师</view>
					<view class="text-color-assist">高级按摩 体验升华</view>
				</view>
			</view>
			<!-- 技师推荐 -->
			<view class="section-2">
				<view class="item" @click="jump('/pages/massagist/massagist')">
					<view class="title">
						<image src="/static/images/home/nav-004.png"></image>
						<view>推荐技师</view>
					</view>
					<view class="tips">灵感商品 立即选购</view>
				</view>
				<view class="item" @click="jump('/pages/massagist/massagist')">
					<view class="title">
						<image src="/static/images/home/nav-003.png"></image>
						<view>新人技师</view>
					</view>
					<view class="tips">50份起送</view>
				</view>
			</view>
			<view class="section-3">
				<image src="https://go.cdn.heytea.com/storage/ad/2020/05/21/bfd57914d80d4671b19f5d0ccc176cd5.jpg" class="image"
				 mode="aspectFill"></image>
				<navigator class="my-integral" open-type="navigate" url="/pages/integrals/mall" hover-class="none">

					<view class="integrals">
						<view>xxx1号女技术</view>
					</view>
					<view class="tips">
						本人擅长养生推拿，精油按摩，手法专业，期待大家来体验
					</view>
				</navigator>
				<navigator class="my-code" open-type="navigate" url="/pages/my/code" hover-class="none">
					<image src="/static/images/home/home_icon_erweima.png"></image>
					<view>健康码</view>
				</navigator>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swipers: [
					"/static/images/5.jpg",
					"/static/images/1.jpg",
					"/static/images/2.jpg",
					"/static/images/3.jpg",
					"/static/images/4.jpg"
				]
			}
		},
		methods: {
			jump: function(page) {
				uni.navigateTo({
					url: page,
					fail(e) {
						uni.switchTab({
							url: page
						})
					}
				});

			}
		}
	}
</script>

<style lang="scss" scoped>
	page {
		max-height: 100%;
	}

	.banner-swiper {
		width: 100%;
		height: 600rpx;

		.banner-swiper-item {
			image {
				width: 100%;
			}
		}
	}

	.content {
		width: 100%;
		padding: 0 30rpx;
		position: relative;
	}

	.section-1 {
		position: relative;
		background-color: $bg-color-white;
		margin-top: -60rpx;
		border-radius: $border-radius-lg;
		padding: 60rpx 0;
		display: flex;
		margin-bottom: 30rpx;
		box-shadow: $box-shadow;

		.item {
			flex: 1;
			flex-shrink: 0;
			display: flex;
			flex-direction: column;
			align-items: center;
			position: relative;

			&:nth-child(1):after {
				content: '';
				position: absolute;
				right: 0;
				top: 0;
				bottom: 0;
				width: 2rpx;
				background-color: $border-color;
			}

			image {
				width: 100rpx;
				margin-bottom: 20rpx;
			}

			.wenyue-font {
				font-size: 48rpx;
				margin-bottom: 10rpx;
			}
		}
	}

	.section-2 {
		display: flex;
		justify-content: space-between;
		margin-bottom: 30rpx;

		.item {
			width: 335rpx;
			background-color: #EAEBEC;
			padding: $spacing-row-lg 0;
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
			border-radius: $border-radius-lg;

			.title {
				width: 100%;
				display: flex;
				align-items: center;
				justify-content: center;
				font-size: $font-size-lg;

				image {
					width: 60rpx;
					height: 60rpx;
					margin-right: 10rpx;
				}
			}

			.tips {
				color: $text-color-assist;
				font-size: $font-size-base;
			}
		}
	}

	.section-3 {
		margin-bottom: 30rpx;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		font-size: $font-size-base;
		color: $text-color-assist;
		padding: 0 10rpx;

		.image {
			width: 150rpx;
			height: 150rpx;
			border-radius: 75rpx;
		}

		.my-integral {
			flex: 1;
			display: flex;
			flex-direction: column;
			margin: 25rpx;

			.integrals {
				display: flex;
				align-items: center;
				font-size: $font-size-lg;
				color: $text-color-base;
				margin-bottom: 10rpx;

				.neutra-font {
					margin-left: 10rpx;
					font-size: 42rpx;
				}
			}
		}

		.my-code {
			display: flex;
			flex-direction: column;
			align-items: center;
			padding: 0 30rpx;
			position: relative;

			image {
				width: 60rpx;
				height: 60rpx;
				margin-bottom: $spacing-col-sm;
			}

			&:before {
				content: " ";
				position: absolute;
				left: 0;
				top: 0;
				bottom: 0;
				border-left: 1rpx solid rgba($color: $border-color, $alpha: 0.6);
			}
		}
	}
</style>
