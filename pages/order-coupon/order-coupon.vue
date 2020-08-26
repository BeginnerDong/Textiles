<template>
	<view>
		
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
					<view class="p-r">
						<!-- <image src="../../static/images/coupons-icon.png" class="wh50 mr-3"></image> -->
						<image src="../../static/images/coupons-icon1.png" class="wh50 mr-3"></image>
						<!-- <image src="../../static/images/coupons-img2.png" class="bky"></image> -->
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
				
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped>
.font-70{font-size: 70rpx;}
.color77{color: #775312;}

.bky{width: 106rpx;height: 81rpx;}
</style>
