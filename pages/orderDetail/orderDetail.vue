<template>
	<view>
		<!-- 待支付 -->
		<!-- <view class="Mgb p-3 flex1 pb-5">
			<view class="color59 line-h flex-1">
				<view class="font-42 color pb-3 font-w">等待支付</view>
				<view>等待买家进行支付~</view>
			</view>
			<image src="../../static/images/theorder-icon4.png" class="zfIcon"></image>
		</view> -->
		<!-- 待发货 -->
		<!-- <view class="Mgb p-3 flex1 pb-5">
			<view class="color59 line-h flex-1">
				<view class="font-42 color pb-3 font-w">等待发货</view>
				<view>卖家将尽快为您发货，请耐心等待！</view>
			</view>
			<image src="../../static/images/theorder-icon5.png" class="fhIcon"></image>
		</view> -->
		<!-- 待收货 -->
		<!-- <view class="Mgb p-3 flex1 pb-5">
			<view class="color59 line-h flex-1">
				<view class="font-42 color pb-3 font-w">等待收货</view>
				<view>您的包裹已寄出，请注意查收~</view>
			</view>
			<image src="../../static/images/theorder-icon7.png" class="shIcon"></image>
		</view> -->
		<!-- 待核销 -->
		<!-- <view class="Mgb p-3 flex1 pb-5">
			<view class="color59 line-h flex-1">
				<view class="font-42 color pb-3 font-w">等待核销</view>
				<view>尽快到自提门店进行核销~</view>
			</view>
			<image src="../../static/images/theorder-icon7.png" class="shIcon"></image>
		</view> -->
		<!-- 已收货/已核销 -->
		<view class="Mgb p-3 flex1 pb-5">
			<view class="color59 line-h flex-1">
				<view class="font-42 color pb-3 font-w">买家已收货</view>
				<!-- <view class="font-42 color pb-3">买家已核销</view> -->
				<view>合作愉快哦~</view>
			</view>
			<image src="../../static/images/theorder-icon3.png" class="shIcon1"></image>
		</view>
		
		
		<view class="bg-white radius20-T p-3 line-h d-flex a-start dz">
			<image src="../../static/images/theorder-icon2.png" class="wh28"></image>
			<view class="addressTxt flex-1 pl-2">
				<view class="font-26 font-w pb-3">张梦瑶 <text class="pl-4">18228926587</text></view>
				<view class="font-24 color9 avoidOverflow">地址：陕西省西安市雁塔区科技路高新大都荟A座2007</view>
			</view>
		</view>
		<view class="f720"></view>
		
		<view class="px-3">
			<view class="py-3 bB-f5">
				<view class="flex1">
					<image src="../../static/images/classification-img.png" class="wh160"></image>
					<view class="flex5 font-30 py-0 flex-1 pl-2 h160">
						<view class="avoidOverflow w510">ROYALCOVER_罗卡芙家纺 浪漫婚典 真丝绣花提花九件套 爱的乐章</view>
						<view class="font-24 color9 flex-1">规格：240*240</view>
						<view class="flex1">
							<view class="price1 font-32 font-w">6980.00</view>
							<view class="font-24 color8">数量：1</view>
						</view>
					</view>
				</view>
				<view class="flex1 pl-180 pt-2">
					<view class="font-24 color9">核销码：</view>
					<image src="../../static/images/theorder-img.png" class="wh80"></image>
				</view>
			</view>
		</view>
		<view class="f720"></view>
		
		<view class="px-3 font-26">
			<view class="flex">
				<view class="color9 pr-4">订单编号：</view>
				<view class="py-3 bB-f5 flex-1">135984568289264</view>
			</view>
			<view class="flex">
				<view class="color9 pr-4">下单时间：</view>
				<view class="py-3 bB-f5 flex-1">2020-07-31 14:09:09</view>
			</view>
			<view class="flex">
				<view class="color9 pr-4">商品数量：</view>
				<view class="py-3 bB-f5 flex-1">1</view>
			</view>
			<view class="flex">
				<view class="color9 pr-4">快递费用：</view>
				<view class="price py-3 bB-f5 flex-1">10</view>
			</view>
			<view class="flex">
				<view class="color9 pr-4">商品总额：</view>
				<view class="price py-3 bB-f5 flex-1">2562.26</view>
			</view>
			<view class="flex">
				<view class="color9 pr-4">满减金额：</view>
				<view class="py-3 bB-f5 flex-1">-￥200</view>
			</view>
		</view>
		<view class="p-3 text-right pb-5">
			实付款： <text class="price1 red font-36 font-w">5689.00</text>
		</view>
		<view class="f720"></view>
		
		<view class="d-flex j-end p-3">
			<view class="btnOrder">取消订单</view>
			<view class="btnOrder order2">去支付</view>
			<view class="btnOrder order2">确认收货</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped>
.color59{color: #593F12;}
.fhIcon{width: 74rpx;height: 72rpx;}
.zfIcon{width: 80rpx;height: 78rpx;}
.shIcon{width: 88rpx;height: 73rpx;}
.shIcon1{width: 74rpx;height: 74rpx;}

.dz{margin-top: -20rpx;}
.price1,.price{color: #222;}
.h160{height: 160rpx;}
.w510{width: 510rpx;}
.red{color: #EA2131;}
.pl-180{padding-left: 180rpx;}

.btnOrder{width: 130rpx;margin-left: 20rpx;}
.order2{border-color: #E6B968;color: #E6B968;}
</style>
