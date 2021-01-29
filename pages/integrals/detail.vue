<template>
	<view class="container">
		<view class="banner-swiper">
			<image src="../../static/images/0.jpg" class="w-100" mode="aspectFill"></image>
		</view>
		
		<view class="header">
			<view class="title">精油开背</view>
			<view class="subtitle">
				<view class="score">￥398</view>
				<!-- <view>金额</view> -->
			</view>
		</view> 
		<view class="content">
			<list-cell :padding="padding" :hover="false" last>
				<view class="row">
					<view class="label">商品类型</view>
					<view class="text">微信支付</view>
				</view>
			</list-cell>
			
			<list-cell :padding="padding" :hover="false" last>
				<view class="row">
					<view class="label">已选技师</view>
					<view class="text">蛋雷</view>
				</view>
			</list-cell>
			<list-cell :padding="padding" :hover="false" last>
				<view class="row">
					<view class="label">有效期限</view>
					<view class="text">2020-2-30 - 2020-2-31</view>
				</view>
			</list-cell>
			
		</view>
		
		<view class="bottom disable">立即付款</view>
	</view>
</template>

<script>	
	export default {
		data() {
			return {
				padding: "20rpx"
			}
		}
	}
</script>

<style lang="scss" scoped>
	.container {
		height: auto;
		background-color: #FFFFFF;
	}
	
	.header {
		padding: 20rpx 30rpx;
		display: flex;
		flex-direction: column;
		border-bottom: 1rpx solid rgba($color: $border-color, $alpha: 0.3);
		
		.title {
			font-size: $font-size-lg;
			margin-bottom: 10rpx;
		}
		.subtitle {
			display: flex;
			align-items: baseline;
			font-size: $font-size-sm;
			color: $text-color-assist;
			.score {
				font-size: $font-size-lg;
				color: $color-primary;
				margin-right: 20rpx;
			}
		}
	}
	
	.content {
		padding-bottom: 100rpx;
		
		.row {
			display: flex;
			align-items: baseline;
			
			.label {
				width: 120rpx;
				font-size: $font-size-medium;
				margin-right: 20rpx;
			}
			
			.text {
				flex: 1;
				font-size: $font-size-sm;
				color: $text-color-assist;
			}		
		}
	}
	
	.bottom {
		position: fixed;
		bottom: 0;
		width: 100%;
		height: 100rpx;
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: $font-size-lg;
		color: $bg-color-white;
		background-color: $color-primary;
		
		&.disabled {
			background-color: #e9d5bb;
		}
	}
</style>
