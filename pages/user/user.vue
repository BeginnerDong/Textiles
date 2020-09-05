<template>
	<view>
		
		<view class="myTop px-3 pt-3">
			<view class="flex">
				<image src="../../static/images/my-img.png" class="wh110 mr-2 radius-5"></image>
				<view>
					<view class="font-34 font-w colorf">哆啦A梦</view>
					<view class="font-24 p-r">
						<image src="../../static/images/my-icon.png" class="vipIcon"></image>
						<view class="p-aX right-0 top-0 pr-1 vipTxt">普通会员</view>
					</view>
				</view>
			</view>
			<view class="mt-4 p-r">
				<image src="../../static/images/my-img1.png" mode="widthFix"></image>
				<view class="p-aXY p-2 flex1">
					<image src="../../static/images/my-icon9.png" class="vip-icon"></image>
					<view class="flex-1 pl-1">会员相关权益</view>
					<view class="btn60"
					@click="Router.navigateTo({route:{path:'/pages/vip-interests/vip-interests'}})">立即查看</view>
				</view>
			</view>
		</view>
		
		<view class="flex bg-white p-3 mb-2 line-h">
			<view class="flex4 p-r w-50 jf"
			@click="Router.navigateTo({route:{path:'/pages/user-integral/user-integral'}})">
				<view class="font-36 font-w pb-2">83236</view>
				<view class="font-24 color8">积分</view>
			</view>
			<view class="flex4 p-r w-50"
			@click="Router.navigateTo({route:{path:'/pages/user-coupon/user-coupon'}})">
				<view class="font-36 font-w pb-2">2</view>
				<view class="font-24 color8">优惠券</view>
			</view>
		</view>
		
		<view class="flex1 bg-white px-3 py-4 line-h mb-2">
			<view class="radius10 p-r"
			@click="Router.navigateTo({route:{path:'/pages/user-order/user-order?type=0'}})">
				<image src="../../static/images/my-icon4.png" class="bg1"></image>
				<view class="px-3 py-4 color7a p-aXY">
					<view class="font-30 font-w">快递订单</view>
					<view class="font-2  pt-2">Delivery order</view>
				</view>
			</view>
			<view class="radius10 p-r"
			@click="Router.navigateTo({route:{path:'/pages/user-order/user-order?type=1'}})">
				<image src="../../static/images/my-icon5.png" class="bg1"></image>
				<view class="px-3 py-4 colorf p-aXY">
					<view class="font-30 font-w">自提订单</view>
					<view class="font-2  pt-2">To the order</view>
				</view>
			</view>
		</view>
		
		<view class="px-3 bg-white">
			<view class="flex1"
			@click="Router.navigateTo({route:{path:'/pages/address/address'}})">
				<image src="../../static/images/my-icon6.png" class="wh36 mr-2"></image>
				<view class="py-4 bB-f5 flex-1 flex1">
					<view>地址管理</view>
					<image src="../../static/images/details-icon2.png" class="jt-icon"></image>
				</view>
			</view>
			<view class="flex1"
			@click="Router.navigateTo({route:{path:'/pages/sales-login/sales-login'}})">
				<image src="../../static/images/my-icon7.png" class="wh36 mr-2"></image>
				<view class="py-4 flex-1 flex1">
					<view>导购员入口</view>
					<image src="../../static/images/details-icon2.png" class="jt-icon"></image>
				</view>
			</view>
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
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/car/car'}})">
				<image src="../../static/images/nabar3.png" mode=""></image>
				<view>购物车</view>
			</view>
			<view class="item on">
				<image src="../../static/images/nabar4-a.png" mode=""></image>
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

<style>page{background-color: #F8F8F8;}</style>
<style scoped>
.myTop{background-color: #272727;}
.vipIcon{width: 160rpx;height: 61rpx;}
.vipTxt{line-height: 61rpx;text-align: right;}
.vip-icon{width: 44rpx;height: 39rpx;}
.btn60{width: 160rpx;}

.color7a{color: #7A5110;}
.bg1{width: 335rpx;height: 140rpx;}
</style>
