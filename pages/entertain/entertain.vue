<template>
	<view class="container">

		<view class="integrals-mall">
			<!-- 分类 -->
			<view>
				<scroll-view class="scroll-view_H" scroll-x="true" @scroll="scroll" scroll-left="120">
					<block v-for="(item, index) in CommodityType" :key="index">
						<view class="scroll-view-item_H  " @click="QueenInfo(item.commodityName)">
							<view class="CommodityTypeBox">
								<button class="CommodityType">
									{{item.commodityName}}
								</button>
							</view>
						</view>
					</block>
				</scroll-view>
			</view>

			<view class="list-wrapper">
				<view class="list">
					<view class="item" @tap="detail(product)">
						<image src="https://p0.meituan.net/merchantpic/fc17b0bcff85c9e5df1e8fac07d6946c_1_b8eb8f1aa8e3ef7a_1_wgSU4pVVn02fbm2BM56%2FqEV3%2F1kk3yyqnKtS%2BV0S1TFDk267h%2FFmebBEkg4z4QD66KhulRSTdnEYUx69WyYXj8fA7KTHaAxAgbJ%2BW2RfwYfJ39exLRbWieOJuzSNSf3K"
						 class="image" mode="widthFix"></image>
						<view class="info">
							<view class="title">商品名称</view>
							<view class="score">
								<view class="value">390</view>
								<view>元</view>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				CommodityType: [{
					id: "1",
					commodityName: "精油Spa"
				}, {
					id: "1",
					commodityName: "按摩推拿"
				}, {
					id: "1",
					commodityName: "足浴"
				}, {
					id: "1",
					commodityName: "能量石"
				}, {
					id: "1",
					commodityName: "采耳"
				}, {
					id: "1",
					commodityName: "牛奶"
				}, {
					id: "1",
					commodityName: "石蜡"
				}, {
					id: "1",
					commodityName: "其他"
				}],
			}
		},
		methods: {
			QueenInfo: function(name) {
				uni.showToast({
					title: name,
					icon: "none",
					position: "bottom"
				})
			},
			scroll: function(e) {

			},
			detail() {

			}
		}
	}
</script>

<style lang="scss" scoped>
	.CommodityTypeBox {
		margin-top: 40rpx;
		margin-left: 10rpx;
		border-radius: 16rpx;
		text-align: center;

		.CommodityType {
			padding: 18rpx 30rpx;
			border-radius: 16rpx;
			background: #eaebec;
			font-family: PingFang SC;
			font-weight: medium;
			font-size: 24rpx;
			line-height: normal;
			letter-spacing: 0rpx;
		}
	}

	/* scroll横向滚动 */
	.scroll-Y {
		height: 300rpx;
	}

	.scroll-view_H {
		white-space: nowrap;
		width: 100%;
	}

	.scroll-view-item {
		height: 300rpx;
		line-height: 300rpx;
		text-align: center;
		font-size: 36rpx;
	}

	.scroll-view-item_H {
		display: inline-block;
		text-align: center;
		font-size: 36rpx;
	}

	/* 滚动条 */
	scroll-view ::-webkit-scrollbar {
		width: 0;
		height: 0;
		background-color: transparent;
	}

	.integrals-mall {
		.list-wrapper {
			background-color: $bg-color-white;

			.list {
				display: flex;
				flex-wrap: wrap;
				padding-bottom: 50rpx;

				.item {
					width: 375rpx;

					.image {
						padding: 20rpx;
						width: 100%;
					}

					.info {
						display: flex;
						flex-direction: column;
						padding: 0 20rpx;

						.title {
							font-size: $font-size-base;
							margin-bottom: 30rpx;
						}

						.score {
							display: flex;
							align-items: baseline;
							font-size: $font-size-sm;
							color: $text-color-assist;

							.value {
								color: $color-primary;
								font-size: $font-size-lg;
							}
						}
					}
				}
			}
		}
	}
</style>
