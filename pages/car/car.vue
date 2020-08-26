<template>
	<view>
		<view class="p-s top-0 p-3 font-26 color8 bg-white bB-f5">全部商品（10）</view>
		
		<view class="bg-white bB-f5 flexX">
			<view class="flex1 p-3 pb-4 w750 flex-shrink">
				<!-- <image src="../../static/images/shopping-icon.png" class="wh36"></image> -->
				<image src="../../static/images/shopping-icon1.png" class="wh36"></image>
				<image src="../../static/images/classification-img.png" class="wh200 ml-2"></image>
				<view class="flex5 font-30 py-0 flex-1 pl-2 h200">
					<view class="avoidOverflow2">ROYALCOVER_罗卡芙家纺 浪漫婚典 真丝绣花提花九件套 爱的乐章</view>
					<view class="font-24 color9 flex-1 line-h pt-1">规格：240*240</view>
					<view class="flex1">
						<view class="price1 font-32 font-w">6980.00</view>
						<view class="count">
							<view class="countIcon"><image src="../../static/images/shopping-icon4.png" class="countIcon1"></image></view>
							<view class="countNum">1</view>
							<view class="countIcon"><image src="../../static/images/shopping-icon3.png" class="countIcon2"></image></view>
						</view>
					</view>
				</view>
			</view>
			<view class="flex4 colorf font-24 Mgb flex-shrink del">
				<image src="../../static/images/shopping-icon2.png" class="del-icon mb-1"></image>
				<view>删除</view>
			</view>
		</view>
		
		
		
		
		<view style="height: 230rpx;"></view>
		<view class="bg-white bT-e1 flex1 font-24 p-fX bot110">
			<view class="flex pl-3 pr-2">
				<image src="../../static/images/shopping-icon1.png" class="wh36 mr-1"></image>
				<view>全选</view>
			</view>
			<view class="flex-1 colorM">删除</view>
			<view class="font-22 color9 px-3">合计：<text class="font-32 price1 font-w">6980.00</text></view>
			<view class="w230 Mgb" 
			@click="Router.navigateTo({route:{path:'/pages/submitOrder/submitOrder'}})">去结算</view>
		</view>
		
		
		<!-- footer -->
		<view class="footer">
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1.png" mode=""></image>
				<view>首页</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/classify/classify'}})">
				<image src="../../static/images/nabar2.png" mode=""></image>
				<view>分类</view>
			</view>
			<view class="item on">
				<image src="../../static/images/nabar3-a.png" mode=""></image>
				<view>购物车</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})">
				<image src="../../static/images/nabar4.png" mode=""></image>
				<view>我的</view>
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

<style>
page{background-color: #f5f5f5;}
</style>
<style scoped>
.h200{height: 200rpx;}
.w750{width: 750rpx;}
.del{height: 270rpx;width: 100rpx;}
.w230{width: 230rpx;line-height: 100rpx;text-align: center;}
.bot110{bottom: 110rpx;}
</style>