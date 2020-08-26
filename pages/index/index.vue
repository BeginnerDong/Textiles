<template>
	<view class="p-r">
		<image src="../../static/images/img.png" mode="widthFix" class="p-aX bgImg"></image>
		
		<!-- banner/搜索框 -->
		<view class="p-r">
			<swiper class="swiper-box" indicator-dots="indicatorDots" autoplay="autoplay" interval="3000" indicator-active-color="#E6B968">
				<block>
					<swiper-item class="swiper-item" >
						<image src="../../static/images/home-banner.png" mode="widthFix" />
					</swiper-item>
				</block>
			</swiper>
			
			<view class="flex font-24 color8 px-3 m-3 p-aX ss"
			@click="Router.navigateTo({route:{path:'/pages/search/search'}})">
				<image src="../../static/images/home-icon.png" class="wh36 mr-3"></image>
				<view>搜索想要找的商品</view>
			</view>
		</view>
		
		<!-- 金刚区 -->
		<view class="font-26 color2 line-h mt-2 p-r flex2">
			<view class="flex4" 
			@click="Router.navigateTo({route:{path:'/pages/integralShop/integralShop'}})">
				<image src="../../static/images/home-icon1.png" class="icon mb-2"></image>
				<view>积分商城</view>
			</view>
			<view class="flex4"
			@click="Router.navigateTo({route:{path:'/pages/store/store'}})">
				<image src="../../static/images/home-icon2.png" class="icon mb-2"></image>
				<view>门店信息</view>
			</view>
			<button open-type="contact" class="line-h font-26 flex4">
				<image src="../../static/images/home-icon3.png" class="icon mb-2"></image>
				<view>联系我们</view>
			</button>
		</view>
		
		<!-- 优惠券 -->
		<view class="mx-3 mt-5 pb-3 p-r">
			<image src="../../static/images/home-img.png" mode="widthFix"></image>
		</view>
		
		<!-- 品牌 -->
		<view class="p-r font-34 font-w flex0 mt-4">
			<view class="p-r pp">
				精选品牌
				<image src="../../static/images/home-icon4.png" class="wh40 p-a"></image>
			</view>
		</view>
		<view class="p-r px-3 flex1 mt-2">
			<view class="flex4" v-for="v in 3 " :key="v">
				<view class="flex0 pp-b radius10 px-3">
					<image src="../../static/images/home-img1.png" mode="widthFix" class="ppIcon"></image>
				</view>
				<view class="flex0 font-18 color2 pt-2 Mgb radius10 pp-y">
					<view>查看商品</view>
					<image src="../../static/images/home-icon5.png" class="jt-icon ml-1"></image>
				</view>
			</view>
		</view>
		
		<!-- 套件系列 -->
		<view class="p-r m-2 mt-3 py-3">
			<image src="../../static/images/home-img3.png" mode="widthFix" class="p-aX"></image>
			<view class="font-34 font-w text-center mt-5 pt-2">套件系列</view>
			<view class="mt-5 flex1 py-2 px-4">
				<view class="w300" @click="Router.navigateTo({route:{path:'/pages/goodDetail/goodDetail'}})">
					<image src="../../static/images/home-img2.png" class="wh300"></image>
					<view class="avoidOverflow2 pt-1">ROYALCOVER_罗卡芙家纺 浪漫婚典 真丝刺绣品牌</view>
					<view class="price1 font-32 font-w pt-2">1620.00</view>
				</view>
				<view class="w300">
					<image src="../../static/images/home-img2.png" class="wh300"></image>
					<view class="avoidOverflow2 pt-1">ROYALCOVER_罗卡芙家纺 浪漫婚典 真丝绣品</view>
					<view class="price1 font-32 font-w pt-2">1620.00</view>
				</view>
			</view>
			<view class="moreBtn font-26 flex0">
				<view>查看更多</view>
				<image src="../../static/images/home-icon6.png" class="jt-icon2"></image>
			</view>
		</view>
		
		<!-- 被芯系列 -->
		<view class="p-r m-2 mt-3 py-3">
			<image src="../../static/images/home-img3.png" mode="widthFix" class="p-aX"></image>
			<view class="font-34 font-w text-center mt-5 pt-2">被芯系列</view>
			<view class="mt-5 flex1 py-2 px-4">
				<view class="w300">
					<image src="../../static/images/home-img2.png" class="wh300"></image>
					<view class="avoidOverflow2 pt-1">ROYALCOVER_罗卡芙家纺 浪漫婚典 真丝刺绣品牌</view>
					<view class="price1 font-32 font-w pt-2">1620.00</view>
				</view>
				<view class="w300">
					<image src="../../static/images/home-img2.png" class="wh300"></image>
					<view class="avoidOverflow2 pt-1">ROYALCOVER_罗卡芙家纺 浪漫婚典 真丝绣品</view>
					<view class="price1 font-32 font-w pt-2">1620.00</view>
				</view>
			</view>
			<view class="moreBtn font-26 flex0">
				<view>查看更多</view>
				<image src="../../static/images/home-icon6.png" class="jt-icon2"></image>
			</view>
		</view>
		
		<!-- 毛巾系列 -->
		<view class="p-r m-2 mt-3 py-3">
			<image src="../../static/images/home-img3.png" mode="widthFix" class="p-aX"></image>
			<view class="font-34 font-w text-center mt-5 pt-2">毛巾系列</view>
			<view class="mt-5 flex1 py-2 px-4">
				<view class="w300">
					<image src="../../static/images/home-img2.png" class="wh300"></image>
					<view class="avoidOverflow2 pt-1">ROYALCOVER_罗卡芙家纺 浪漫婚典 真丝刺绣品牌</view>
					<view class="price1 font-32 font-w pt-2">1620.00</view>
				</view>
				<view class="w300">
					<image src="../../static/images/home-img2.png" class="wh300"></image>
					<view class="avoidOverflow2 pt-1">ROYALCOVER_罗卡芙家纺 浪漫婚典 真丝绣品</view>
					<view class="price1 font-32 font-w pt-2">1620.00</view>
				</view>
			</view>
			<view class="moreBtn font-26 flex0">
				<view>查看更多</view>
				<image src="../../static/images/home-icon6.png" class="jt-icon2 ml-1"></image>
			</view>
		</view>
		
		
		
		
		<view style="height: 130rpx;"></view>
		<!-- footer -->
		<view class="footer">
			<view class="item on" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1-a.png" mode=""></image>
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
				Router:this.$Router,
				is_show: false,
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				self.$apis.orderGet(postData, callback);
			}
		}
	};
</script>

<style scoped>
.swiper-box,.swiper-item{height: 410rpx;}
.ss{height: 60rpx;line-height: 60rpx;border-radius: 30rpx;background-color: rgba(255,255,255,0.5);top: 0;}
.icon{width: 51rpx;height: 54rpx;}
.bgImg{margin-top: 380rpx;}

.pp image{top: -22rpx;right: -32rpx;}
.pp-b{width: 210rpx;height: 100rpx;background-color: #2A2A2A;z-index: 5;}
/* .ppIcon{height: 20rpx;} */
.pp-y{width: 180rpx;height: 58rpx;margin-top: -20rpx;}

</style>