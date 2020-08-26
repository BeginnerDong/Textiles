<template>
	<view>
		
		<view class="list mb-2 shadowM">
			<view class="li" :class="liCurr==0?'on':''" @click="changeLi(0)">未使用</view>
			<view class="li" :class="liCurr==1?'on':''" @click="changeLi(1)">已使用</view>
			<view class="li" :class="liCurr==2?'on':''" @click="changeLi(2)">已过期</view>
		</view>
		
		<!-- 优惠券 -->
		<view class="p-3">
			<view class="mb-3 p-r">
				<image src="../../static/images/coupons-img.png" mode="widthFix" v-show="liCurr==0"></image>
				<image src="../../static/images/coupons-img1.png" mode="widthFix" v-show="liCurr!=0"></image>
				<view class="flex1 p-aXY p-3 pb-4">
					<view class="font-26 font-w pl-5" 
					:class="liCurr==0?'colorR':'color8'">￥ <text class="font-70">100</text></view>
					<view class="font-20 line-h flex-1 pl-4" :class="liCurr==0?'color77':'color9'">
						<view class="font-28 pb-2">无门槛优惠券</view>
						<view class="pb-2">领取后30天内有效</view>
						<view>满600元使用</view>
					</view>
				</view>
				<image src="../../static/images/coupons-icon4.png" 
				class="wh80 p-a top-0 right-10"  v-show="liCurr==0"></image>
				<image src="../../static/images/coupons-icon5.png" 
				class="wh80 p-a top-0 right-10"  v-show="liCurr==1"></image>
				<image src="../../static/images/coupons-icon6.png" 
				class="wh80 p-a top-0 right-10"  v-show="liCurr==2"></image>
			</view>
		</view>
		
		<!-- 暂无优惠券展示 -->
		<!-- <view @click="Router.navigateTo({route:{path:'/pages/index/index'}})">
			<image src="../../static/images/coupons-icon9.png" class="null"></image>
			<view class="btn80 Mgb">去逛逛</view>
		</view> -->
		
		<view class="flex0 pt-3">
			<image src="../../static/images/coupons-icon8.png" class="line"></image>
			<view class="px-2">领取优惠券</view>
			<image src="../../static/images/coupons-icon7.png" class="line"></image>
		</view>
		<view class="p-3">
			<view class="mb-3 p-r" v-for="v in 3" :key="v">
				<image src="../../static/images/coupons-img.png" mode="widthFix"></image>
				<view class="flex1 p-aXY p-3 pb-4">
					<view class="font-26 colorR font-w pl-5">￥ <text class="font-70">100</text></view>
					<view class="color77 font-20 line-h flex-1 pl-4">
						<view class="font-28 pb-2">无门槛优惠券</view>
						<view class="pb-2">领取后30天内有效</view>
						<view>满600元使用</view>
					</view>
					<view class="p-r"
					@click="Router.navigateTo({route:{path:'/pages/VIP-infomation/VIP-infomation'}})">      
						<image src="../../static/images/coupons-icon3.png" class="wh110"></image>
						<view class="p-aXY flex0 colorf">领取</view>
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
				Router:this.$Router,
				liCurr:0
			}
		},
		methods: {
			
			changeLi(i){
				const self = this;
				self.liCurr = i
			}
			
		}
	}
</script>

<style>
page{background-color: #f5f5f5}
</style>
<style scoped>
.li{width:33.33%;}
.null{width: 119rpx;height: 114rpx;margin: 100rpx auto 50rpx;}
.btn80{line-height: 60rpx;width: 160rpx;margin: 0 auto 50rpx;font-size: 26rpx;}
.font-70{font-size: 70rpx;}
.color77{color: #775312;}
.right-10{right: 10rpx;}
</style>