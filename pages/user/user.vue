<template>
	<view>
		
		<view class="myTop px-3 pt-3" style="height: 280rpx;">
			<view class="flex">
				<image :src="userData.headImgUrl?userData.headImgUrl:''" class="wh110 mr-2 radius-5"></image>
				<view>
					<view class="font-34 font-w colorf">{{userData.nickname?userData.nickname:''}}</view>
					<view class="font-24 p-r" v-if="userData.info&&userData.info.level==0">
						<image src="../../static/images/my-icon.png" class="vipIcon"></image>
						<view class="p-aX right-0 top-0 pr-1 vipTxt">普通会员</view>
					</view>
					<view class="font-24 p-r" v-if="userData.info&&userData.info.level==1">
						<image src="../../static/images/my-icon1.png" class="vipIcon"></image>
						<view class="p-aX right-0 top-0 pr-1 vipTxt">黄金会员</view>
					</view>
					<view class="font-24 p-r" v-if="userData.info&&userData.info.level==2">
						<image src="../../static/images/my-icon2.png" class="vipIcon"></image>
						<view class="p-aX right-0 top-0 pr-1 vipTxt">钻石会员</view>
					</view>
					<view class="font-24 p-r" v-if="userData.info&&userData.info.level==3">
						<image src="../../static/images/my-icon3.png" class="vipIcon"></image>
						<view class="p-aX right-0 top-0 pr-1 vipTxt">皇冠会员</view>
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
				<view class="font-36 font-w pb-2">{{userData.info?userData.info.score:0}}</view>
				<view class="font-24 color8">积分</view>
			</view>
			<view class="flex4 p-r w-50"
			@click="Router.navigateTo({route:{path:'/pages/user-coupon/user-coupon'}})">
				<view class="font-36 font-w pb-2">{{userData.userCoupon?userData.userCoupon.length:0}}</view>
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
			@click="Router.navigateTo({route:{path:'/pages/vip-interests/vip-interests'}})">
				<image src="../../static/images/my-icon0.png" class="wh36 mr-2"></image>
				<view class="py-4 bB-f5 flex-1 flex1">
					<view>会员权益</view>
					<image src="../../static/images/details-icon2.png" class="jt-icon"></image>
				</view>
			</view>
			<view class="flex1"
			@click="Router.navigateTo({route:{path:'/pages/address/address'}})">
				<image src="../../static/images/my-icon6.png" class="wh36 mr-2"></image>
				<view class="py-4 bB-f5 flex-1 flex1">
					<view>地址管理</view>
					<image src="../../static/images/details-icon2.png" class="jt-icon"></image>
				</view>
			</view>
			<view class="flex1"
			@click="checkLogin">
				<image src="../../static/images/my-icon7.png" class="wh36 mr-2"></image>
				<view class="py-4 flex-1 flex1">
					<view>导购员入口</view>
					<image src="../../static/images/details-icon2.png" class="jt-icon"></image>
				</view>
			</view>
			<button class="flex1 font-28" open-type="contact">
				<image src="../../static/images/home-icon3.png" class="wh36 mr-2"></image>
				<view class="py-4 flex-1 flex1">
					<view>联系我们</view>
					<image src="../../static/images/details-icon2.png" class="jt-icon"></image>
				</view>
			</button>
		</view>
		 
		<!-- <button open-type="contact" style="position: fixed;bottom: 40%;right: 2%;z-index: 10">
			<image src="../../static/images/kefu.png" style="width: 70rpx;height: 70rpx;">
			<view class="colorM font-28">客服</view>
		</button> -->
		
		<view style="height: 130rpx;"></view>
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
				Router:this.$Router,
				userData:{}
			}
		},
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getUserData'], self);
		},
		methods: {
			
			checkLogin(){
				const self = this;
				if(uni.getStorageSync('sales_token')){
					self.Router.navigateTo({route:{path:'/pages/sales-enter/sales-enter'}})
				}else{
					self.Router.navigateTo({route:{path:'/pages/sales-login/sales-login'}})
				}
			},
			
			getUserData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.getAfter = {
					userCoupon:{
						tableName:'UserCoupon',
						middleKey:'user_no',
						key:'user_no',
						searchItem:{
							status:1,
							use_step:1
						},
						condition:'='
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0];
						self.userData.info.score = parseInt(self.userData.info.score)
					};
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},
		}
	}
</script>

<style>page{background-color: #F8F8F8;}</style>
<style scoped>
.myTop{background-color: #272727;}
.vipIcon{width: 160rpx;height: 61rpx;}
.vipTxt{line-height: 61rpx;padding-left: 50rpx;}
.vip-icon{width: 44rpx;height: 39rpx;}
.btn60{width: 160rpx;}

.color7a{color: #7A5110;}
.bg1{width: 335rpx;height: 140rpx;}
</style>
