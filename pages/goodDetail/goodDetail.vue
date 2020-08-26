<template>
	<view>
		<!-- 轮播 -->
		<swiper class="swiper-box" indicator-dots="indicatorDots" autoplay="autoplay" interval="3000" indicator-active-color="#E6B968">
			<block>
				<swiper-item class="swiper-item" >
					<image src="../../static/images/details-img.png" />
				</swiper-item>
			</block>
		</swiper>
		
		<!-- 详情 -->
		<view class="p-3 flex1">
			<view class="price1 colorR font-40">6980.00</view>
			<!-- <view class="colorR font-40">99 <text class="font-22">积分</text></view> -->      <!-- 积分商品展示 -->
			<button class="flex4 font-22">        <!-- 积分商品不展示分享 -->
				<image src="../../static/images/details-icon.png" class="wh30 mb-2"></image>
				<view>分享</view>
			</button>
		</view>
		<view class="font-32 font-w color2 mx-3 pb-3 bB-f5">ROYALCOVER_罗卡芙家纺 浪漫婚典 真丝刺绣品牌</view>
		<view class="flex p-3 line-h">
			<view class="color8 pr-5">配送</view>
			<view class="flex1 pr-3">
				<image src="../../static/images/details-icon1.png" class="wh20 mr-1"></image>
				<view>快递配送</view>
			</view>
			<view class="flex1">
				<image src="../../static/images/details-icon1.png" class="wh20 mr-1"></image>
				<view>快递配送</view>
			</view>
		</view>
		<view class="f8-16"></view>
		
		<view class="flex p-3 line-h">
			<view class="color8 pr-5">请选择</view>
			<view class="flex-1 pr-3">规格 数量</view>
			<image src="../../static/images/details-icon2.png" class="jt-icon"></image>
		</view>
		<view class="f8-16"></view>
		
		<view>      <!-- 积分商品展示 -->
			<view class="color8 p-3">积分兑换说明</view>
			<view class="px-3 pb-3">1、不限制兑换个数</view>
		</view>
		<view class="f8-16"></view>
		
		<view>
			<view class="color8 p-3">详情</view>
			<view class="px-3 pb-3">商品名称  水星......</view>
			<image src="../../static/images/details-img1.png" mode="widthFix"></image>
		</view>
		
		
		<!-- 正常购买按钮 -->
		<!-- <view style="height: 100rpx;"></view> -->
		<!-- <view class="p-fX bottom-0 bT-f5 flex1 bg-white">
			<view class="flex flex-1">
				<view class="flex4 font-22 bR-f5 w145 line-h" @click="Router.back({route:{delta:1}})">
					<image src="../../static/images/details-icon3.png" class="fh-icon mb-1"></image>
					<view>返回</view>
				</view>
				<view class="flex4 font-22 w145 line-h" @click="Router.navigateTo({route:{path:'/pages/car/car'}})">
					<image src="../../static/images/details-icon4.png" class="wh40 mb-1"></image>
					<view>购物车</view>
				</view>
			</view>
			<view class="btnBox flex">
				<view class="btn w-50 colorf">加入购物车</view>
				<view class="btn w-50 btn1 Mgb">立即购买</view>
			</view>
		</view> -->
		
		<!-- 积分商品兑换按钮 -->
		<view style="height: 170rpx;"></view>
		<view class="p-fX bottom-0 bT-f5">
			<view class="font-24 colorf jf text-center bg-7e">您的可用积分不足，去看看其他商品吧~</view>
			<view class="flex1 bg-white">
				<view class="flex">
					<view class="flex4 font-22 bR-f5 w145 line-h"
					@click="Router.back({route:{delta:1}})">
						<image src="../../static/images/details-icon3.png" class="fh-icon mb-1"></image>
						<view>返回</view>
					</view>
				</view>
				<view class="btnBox flex flex-1">
					<view class="btn w-100 btn1 Mgb">立即兑换</view>       <!-- 积分不足是增加gb-f7类名 -->
				</view>
			</view>
		</view>
		
		
		<!-- 规格 -->
		<view class="bg-mask" v-show="gg_show">
			<view class="gg p-3 bg-white p-aX bottom-0">
				<view class="flex pb-2">
					<image src="../../static/images/details-img.png" class="wh200"></image>
					<view class="flex-1 pl-2">
						<view class="price1 font-40 pb-2">6980.00</view>
						<view class="font-24 color8">请选择规格</view>
					</view>
				</view>
				<view class="font-26 color2 py-3">
					<view>规格</view>
					<view class="flex flex-wrap signBox">
						<view class="tag on">240*240cm</view>
						<view class="tag">240*240cm</view>
					</view>
				</view>
				<view class="flex1 pt-2">
					<view>数量</view>
					<view class="count">
						<view class="countIcon"><image src="../../static/images/shopping-icon4.png" class="countIcon1"></image></view>
						<view class="countNum">1</view>
						<view class="countIcon"><image src="../../static/images/shopping-icon3.png" class="countIcon2"></image></view>
					</view>
				</view>
				
				<view class="p-aX bottom-0 flex">
					<view class="btn w-50 bg3c colorf">加入购物车</view>
					<view class="btn w-50 Mgb">立即购买</view>
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
				gg_show:false
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped>
.swiper-box,.swiper-item,.swiper-item image{width: 750rpx;height: 750rpx;}
.btnBox{width: 460rpx;}
.w145{width: 145rpx;}

.gg{height: 800rpx;}
.gg .wh200{margin-top: -100rpx;}
.gg .tag{width: 200rpx;line-height: 64rpx;text-align: center;border-radius: 10rpx;border: 1px solid #e5e5e5;margin: 30rpx 30rpx 0 0;}
.gg .on{background-color: #E6B968;border: none;}
.gg .signBox{max-height: 330rpx;overflow-y: auto;}
.bg-d7{background-color: #d7d7d7;}
.bg-7e{background-color: #7F7F7F;}
.jf{line-height: 70rpx;}
</style>
