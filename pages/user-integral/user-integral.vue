<template>
	<view>
		
		<view class="mx-5 mt-5 p-3 h233 line-h p-r bB-f5">
			<image src="../../static/images/integra-img.png" mode="widthFix" class="p-aX top-0"></image>
			<view class="p-r">
				<view class="font-24 pt-3 pb-2">积分</view>
				<view class="font-80 font-w">7812</view>
			</view>
		</view>
		
		<view class="flex1 py-2 bB-f5 p-r z10">
			<view class="flex0 w-50 p-r jf"
			@click="Router.navigateTo({route:{path:'/pages/integralShop/integralShop'}})">
				<image src="../../static/images/integra-icon.png" class="wh28 mr-1"></image>
				<view>积分商城</view>
			</view>
			<view class="flex0 w-50"
			@click="Router.navigateTo({route:{path:'/pages/user-integralExchange/user-integralExchange'}})">
				<image src="../../static/images/integra-icon1.png" class="wh28 mr-1"></image>
				<view>兑换记录</view>
			</view>
		</view>
		
		<view class="flex0 py-3">
			<image src="../../static/images/coupons-icon8.png" class="line"></image>
			<view class="px-2 color8">积分明细</view>
			<image src="../../static/images/coupons-icon7.png" class="line"></image>
		</view>
		
		<view class="px-3">
			<view class="flex1">
				<image src="../../static/images/integra-icon2.png" class="wh80"></image>
				<view class="flex-1 py-3 bB-f5 flex1 ml-2 line-h">
					<view>
						<view>完成订单</view>
						<view class="font-24 color9 pt-2">2020-08-12 09:09:28</view>
					</view>
					<view class="colorR font-32 font-w">+13</view>
				</view>
			</view>
			<view class="flex1">
				<image src="../../static/images/integra-icon3.png" class="wh80"></image>
				<view class="flex-1 py-3 bB-f5 flex1 ml-2 line-h">
					<view>
						<view>积分兑换商品</view>
						<view class="font-24 color9 pt-2">2020-08-12 09:09:28</view>
					</view>
					<view class="font-32 font-w">-99</view>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped>
.h233{height: 233rpx;}
.font-80{font-size: 80rpx;}
</style>
