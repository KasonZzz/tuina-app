<template>
	<view class="container">
		<view class="header">
			<!-- 搜索栏 begin -->
			<view class="search-box">
				<view class="search-input" @tap="showSearch=true">
					<image src="/static/images/common/search-icon.png" class="search-icon"></image>
					<view>搜索</view>
				</view>
			</view>
			<!-- 搜索栏 end -->
			
			<!-- 滚动公告栏 begin -->
			<view class="notices">
				<swiper class="swiper" autoplay vertical :interval="3000" :duration="1000" circular>
					<swiper-item v-for="(notice, index) in notices" :key="index">
						<view class="swiper-item">
							<image :src="notice.image" class="image"></image>
							<view class="content">{{ notice.content }}</view>
						</view>
					</swiper-item>
				</swiper>
				<view class="more">
					<text>更多</text>
					<image src="/static/images/common/gray_arrow_down.png" class="down-icon"></image>
				</view>
			</view>
		</view>
		<!-- 滚动公告栏 end -->
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
		
		
		
		<view class="section-3">
				<image src="https://go.cdn.heytea.com/storage/ad/2020/05/21/bfd57914d80d4671b19f5d0ccc176cd5.jpg" class="image" mode="aspectFill"></image>
				<navigator class="my-integral" open-type="navigate" url="/pages/integrals/mall" hover-class="none">
					
					<view class="integrals">
						<view>xxx1号女技师</view>
						<view class="mass-status">正在听单</view>
					</view> 
					<view class="tips">
						本人擅长养生推拿，精油按摩，手法专业，期待大家来体验
					</view> 
				</navigator>
				<navigator class="my-code" open-type="navigate" url="/pages/my/code" hover-class="none">
					<image src="../../static/images/home/home_icon_erweima.png"></image>
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
				notices: [],
			}
		},
		async onLoad() {
			this.notices = await this.$api('notices')
		},
		methods: {
			QueenInfo: function(name){
				uni.showToast({
					title:name,
					icon:"none",
					position:"bottom"
				})
			},
			scroll: function(e) {
			
			},
		}
	}
</script>

<style lang="scss">
	@import '../index/index.scss';

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
	
	.section-3 {
		margin-bottom: 30rpx;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		font-size: $font-size-base;
		color: $text-color-assist;
		padding: 0 10rpx;
		.image{
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
				.mass-status{
					margin-left: auto;
					border-radius: 25rpx;
					background: #09BB07;
					font-size: $font-size-base;
					color: #FFFFFF;
					padding: 8rpx;
				}
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
