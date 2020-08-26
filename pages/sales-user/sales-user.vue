<template>
	<view>
		
		<view class="px-2">
			<image src="../../static/images/thesalesman-img1.png" mode="widthFix"></image>
			
			<view class="p-aXY p-5 mx-2">
				<view class="font-26 colorf mt-2">推广用户（28个）</view>
				
				<view class="flex flex-wrap mt-4 ">
					<image src="../../static/images/thesalesman-icon3.png" class="wh70"></image>
					<image src="../../static/images/thesalesman-icon4.png" class="wh70" v-for="v in 5" :key="v"></image>
				</view>
			</view>
		</view>
		
		<view class="flex0 pt-3">
			<image src="../../static/images/coupons-icon8.png" class="line"></image>
			<view class="px-2 color8">交易记录</view>
			<image src="../../static/images/coupons-icon7.png" class="line"></image>
		</view>
		
		<view class="px-3">
			<view class="flex1">
				<image src="../../static/images/thesalesman-icon4.png" class="wh80"></image>
				<view class="flex-1 py-3 bB-f5 flex1 ml-2 line-h">
					<view>
						<view>张丹</view>
						<view class="font-24 color9 pt-2">2020-08-12 09:09:28</view>
					</view>
					<view class="font-32 font-w price">5642</view>
				</view>
			</view>
			<view class="flex1">
				<image src="../../static/images/thesalesman-icon3.png" class="wh80"></image>
				<view class="flex-1 py-3 bB-f5 flex1 ml-2 line-h">
					<view>
						<view>张丹</view>
						<view class="font-24 color9 pt-2">2020-08-12 09:09:28</view>
					</view>
					<view class="font-32 font-w price">9586</view>
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
.wh70{margin-left: -20rpx;border: 1px solid #f5f5f5;border-radius: 50%;margin-bottom: 15rpx;}
.wh70:nth-child(1),.wh70:nth-child(13n){margin-left: 0;}
.price{color: #222;}
</style>
