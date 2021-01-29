<template>
	<view class="pageFlex">
		<view class="topBox">
			<view class="top1">
				<view class="yue">
					余额
				</view>
				<view @click="toIncome" class="income icon iconfont iconshouruzengchang">
				</view>
			</view>
			
			<view class="numBox">
				<view class="num">
					￥1314520
				</view>
				<view class="statistics">
					<view class="statisticsBox">
						<view class="statisticsLabel">
							本月收入
						</view>
						<view class="statisticsValue">
							￥600
						</view>
					</view>
					<view class="statisticsBox">
						<view class="statisticsLabel">
							历史收入
						</view>
						<view class="statisticsValue">
							￥600
						</view>
					</view>
					<view class="statisticsBox">
						<view class="statisticsLabel">
							提现总额
						</view>
						<view class="statisticsValue">
							￥600
						</view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="priceBox">
			<view class="money">
				￥10
			</view>
			<view class="money">
				￥30
			</view>
			<view class="money">
				￥50
			</view>
			<view class="money">
				￥100
			</view>
			<view class="money">
				￥500
			</view>
			<view class="money">
				<input class="uni-input uni-center menuValue" type="number" placeholder-class="uni-center" placeholder="自定义" />
			</view>
		</view>
		
		
		<view class="payBox">
			<view>
				支付方式
			</view>
			
			<view class="aliPay">
				<view class="icon iconfont iconchangyonglogo30 ">
					
				</view>
				<view class="aliPayItem">
					支付宝
				</view>
				<view class="radioBox">
					<label class="radio"><radio value="r1" checked="true" /></label>

				</view>
			</view>
			<hr class="line"/>
			<view class="aliPay">
				<view class="icon iconfont iconweixinzhifu">
					
				</view>
				<view class="aliPayItem">
					微信
				</view>
				<view class="radioBox">
					<label class="radio"><radio value="r1" checked="true" /></label>
				</view>
			</view>
			<hr class="line"/>
			
		</view>
		
		<button class="topUp" type="primary">立即充值</button>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			toIncome(){
				
			}
		}
	}
</script>

<style>
	.pageFlex{
		display: flex;
		flex-direction: column;
	}
	.topBox{
		margin: 30rpx;
		width: 700rpx;
		border-radius: 30rpx;
		background: #eaebec;
		font-size: 35rpx;
		display: flex;
		flex-direction: column;
		color: #00000;
	}
	.top1{
		display: flex;
	}
	.yue{
		margin: 15rpx 15rpx 15rpx 75rpx;
	}
	.income{

		margin: 15rpx;
		margin-left: auto;
	}	
	.numBox{
		margin: 15rpx 0rpx 50rpx 0rpx;
		display: flex;
	}
	.num{
		margin: 35rpx;
		font-size: 38rpx;
	}
	.statistics{
		flex:1;
		display: flex;
		flex-direction: column;
		font-weight: 100;
		font-size: 15rpx;
		letter-spacing: 0px;
		text-align: center;

	}
	.statisticsBox{
		flex:1;
		display: flex;
		color: #00000;
	}
	.statisticsLabel{
		
		margin: 5rpx;
		width: 50%;
		text-align: right;
	}
	.statisticsValue{
		margin: 5rpx;
		width: 50%;
		text-align: center;
	}
	.priceBox{
		margin: 30rpx;
		width: 700rpx;
		font-size: 35rpx;
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: space-between;
		color: #00000;
	}
	.money{
		margin-top:50rpx;
		border-radius: 30rpx;
		background: #eaebec;
		width: 200rpx;
		height: 100rpx;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.menuValue{
		background: none;
	}
	.line{
		border: 1rpx solid #3c3942;
		box-shadow: 0rpx 4rpx 4rpx 0rpx #27242d;
	}
	.payBox{
		margin: 30rpx;
		width: 700rpx;
		display: flex;
		flex-direction: column;
		color: #FFFFFF;
	}
	.aliPay{
		margin-top: 60rpx;
		display: flex;
	}
	.iconchangyonglogo30{
		color: #007AFF;
		font-size: 65rpx;
	}
	.iconweixinzhifu{
		color: #09BB07;
		font-size: 55rpx;
	}
	
	.aliPayItem{
		flex: 1;
		text-align: center;
		align-self: center;
	}
	.radioBox{
		text-align: right;
		  align-self: center;
	}
	.topUp{
		margin: 50rpx;
		width: 650rpx;
		letter-spacing: 25rpx;
		border-radius: 19px;
		background: #53B175;
	}
	 
</style>
