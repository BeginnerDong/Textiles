<template>
	<view>
		
		<view class="m-3 bg-white radius10 color2 line-h p-r">
			<image src="../../static/images/submit-img.png" mode="widthFix" class="bgAdd"
			v-show="tabCurr==0"></image>
			<image src="../../static/images/submit-img2.png" mode="widthFix" class="bgAdd"
			v-show="tabCurr==1"></image>
			<view class="flex text-center font-30 radius10 p-r line-h pt-1">
				<view class="w-50 pb-3 pt-1" @click="changeTab(0)">快递配送</view>
				<view class="w-50 pb-3 pt-1" @click="changeTab(1)">到店自提</view>
			</view>
			<view class="flex1 px-3 py-4 p-r"
			@click="Router.navigateTo({route:{path:'/pages/selfRaising/selfRaising'}})">
				<view class="addressTxt">
					<view class="font-30 font-w avoidOverflow">陕西省西安市雁塔区科技路高新大都荟A座2007</view>
					<view class="font-26 color9 pt-3">张梦瑶 <text class="pl-4">18228926587</text></view>
				</view>
				<image src="../../static/images/details-icon2.png" class="jt-icon"></image>
			</view>
			<view class="flex1 py-3 mx-3 bT-f5 p-r" v-show="tabCurr==1">
				<input type="text" value="" placeholder="收货人姓名" />
				<input type="text" value="" placeholder="电话" />
			</view>
		</view>
		
		<view class="bg-white p-3 mx-3 radius10">
			<view class="flex1 pb-3 bB-f5 w750 flex-shrink">
				<image src="../../static/images/classification-img.png" class="wh200"></image>
				<view class="flex5 font-30 py-0 flex-1 pl-2 h200">
					<view class="avoidOverflow2">ROYALCOVER_罗卡芙家纺 浪漫婚典 真丝绣花提花九件套 爱的乐章</view>
					<view class="font-24 color9 flex-1 line-h pt-1">规格：240*240</view>
					<view class="price1 font-32 font-w">6980.00</view>    <!-- 正常订单 -->
					<!-- <view class="font-32 font-w colorR">99 <text class="font-22">积分</text></view> -->      <!-- 积分订单 -->
				</view>
			</view>
			<view class="flex1 pt-3">
				<view class="color8">购买数量</view>
				<view class="count">
					<view class="countIcon"><image src="../../static/images/shopping-icon4.png" class="countIcon1"></image></view>
					<view class="countNum">1</view>
					<view class="countIcon"><image src="../../static/images/shopping-icon3.png" class="countIcon2"></image></view>
				</view>
			</view>
		</view>
		
		<view class="bg-white px-3 mx-3 mt-2 radius10 line-h">
			<!-- 普通订单展示优惠券 -->
			<view class="flex1 py-4 bB-f5"
			@click="Router.navigateTo({route:{path:'/pages/order-coupon/order-coupon'}})">
				<view class="color8">优惠券</view>
				<view class="flex">
					<view>满1000件200</view>
					<image src="../../static/images/details-icon2.png" class="jt-icon ml-1"></image>
				</view>
			</view>
			<view class="flex1 py-4">
				<view class="color8">运费</view>
				<view>￥10</view>
			</view>
		</view>
		
		<view class="bg-white bT-e1 flex1 p-fX bottom-0">
			<view class="font-22 color9 px-3">合计：
				<!-- <text class="font-32 price1 font-w">6980.00</text> -->
				<text class="font-32 font-w colorR">99 <text class="font-22">积分</text></text>
			</view>
			<view class="w230 Mgb font-30" >提交订单</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				tabCurr:1
			}
		},
		methods: {
			
			changeTab(i){
				const self = this;
				self.tabCurr = i
			}
			
		}
	}
</script>

<style>
page{background-image: linear-gradient(to bottom, #E6B968, #f5f5f5 40%);background-color: #f5f5f5;}
</style>
<style scoped>
.addressTxt{width: 530rpx;}
.bgAdd{position: absolute;top: 0;margin-top: -10rpx;}
.h200{height: 200rpx;}
.w230{width: 230rpx;line-height: 100rpx;text-align: center;}
input{width: 300rpx;height: 60rpx;text-align: center;font-size: 24rpx;border-radius: 10rpx;border: 1px solid #e1e1e1;}
</style>
