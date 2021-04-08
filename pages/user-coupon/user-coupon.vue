<template>
	<view>
		
		<view class="list mb-2 shadowM z100">
			<view class="li" :class="liCurr==0?'on':''" @click="changeLi(0)">未使用</view>
			<view class="li" :class="liCurr==1?'on':''" @click="changeLi(1)">已使用</view>
			<view class="li" :class="liCurr==2?'on':''" @click="changeLi(2)">已过期</view>
		</view>
		
		<!-- 优惠券 -->
		<view class="p-3">
			<view class="mb-3 p-r" v-if="userCoponData.length>0" v-for="(item,index) in userCoponData" :key="index">
				<image src="../../static/images/coupons-img.png" mode="widthFix" v-show="liCurr==0"></image>
				<image src="../../static/images/coupons-img1.png" mode="widthFix" v-show="liCurr!=0"></image>
				<view class="flex1 p-aXY p-3 pb-4">
					<view class="font-26 font-w pl-5" 
					:class="liCurr==0?'colorR':'color8'">￥ <text class="font-70">{{item.value}}</text></view>
					<view class="font-20 line-h flex-1 pl-4" :class="liCurr==0?'color77':'color9'">
						<view class="font-28 pb-2">{{item.title}}</view>
						<view class="pb-2">有效期至：{{Utils.timeto(item.invalid_time,'ymd')}}</view>
						<view>满{{item.condition}}元使用</view>
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
		<view @click="Router.redirectTo({route:{path:'/pages/index/index'}})" v-if="userCoponData.length==0">
			<image src="../../static/images/coupons-icon9.png" class="null"></image>
			<view class="btn80 Mgb">去逛逛</view>
		</view>
		
		<view class="flex0 pt-3">
			<image src="../../static/images/coupons-icon8.png" class="line"></image>
			<view class="px-2">领取优惠券</view>
			<image src="../../static/images/coupons-icon7.png" class="line"></image>
		</view>
		<view class="p-3">
			<view class="mb-3 p-r" v-for="(item,index) in couponData" :key="index">
				<image src="../../static/images/coupons-img.png" mode="widthFix"></image>
				<view class="flex1 p-aXY p-3 pb-4">
					<view class="font-26 colorR font-w pl-5">￥ <text class="font-70">{{item.value}}</text></view>
					<view class="color77 font-20 line-h flex-1 pl-4">
						<view class="font-28 pb-2">{{item.title}}</view>
						<view class="pb-2">领取后{{item.valid_time}}天内有效</view>
						<view>满{{item.condition}}元使用</view>
					</view>
					<view class="p-r"
					@click="submit(index)">      
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
				liCurr:0,
				couponData:[],
				searchItem:{
					use_step:1
				},
				userCoponData:[],
				Utils:this.$Utils
			}
		},
		onLoad(){
			const self = this;
			self.$Utils.loadAll(['getCouponData','getUserCouponData'], self);
		},
		
		onShow() {
			const self = this;
			self.getUserInfoData()
		},
		
		methods: {
			
			changeLi(i){
				const self = this;
				if(self.liCurr!=i){
					self.liCurr = i
					if(self.liCurr==0){
						self.searchItem.use_step=1
					}else if(self.liCurr==1){
						self.searchItem.use_step=2
					}else if(self.liCurr==2){
						self.searchItem.use_step=-1
					}
					self.userCoponData= [];
					self.getUserCouponData()
				}
			},
			
			getUserInfoData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userInfoData = res.info.data[0];
					};
				};
				self.$apis.userInfoGet(postData, callback);
			},
			
			getUserCouponData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = self.$Utils.cloneForm(self.searchItem)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userCoponData = res.info.data
					}
					self.$Utils.finishFunc('getUserCouponData');
				};
				self.$apis.userCouponGet(postData, callback);
			},
			
			getCouponData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.couponData = res.info.data
					}
					self.$Utils.finishFunc('getCouponData');
				};
				self.$apis.couponGet(postData, callback);
			},
			
			submit(index){
				const self = this;
				if(self.userInfoData.phone==''){
					self.Router.navigateTo({route:{path:'/pages/VIP-infomation/VIP-infomation'}})
				}else{
					self.couponAdd(index)
				}
			},
			
			couponAdd(index) {
				const self = this;
				self.orderList = [{
					coupon_id: self.couponData[index].id,
					count: 1,
					type: self.couponData[index].type,
				}];
				const postData = {
					tokenFuncName: 'getProjectToken',
				};
				postData.couponList = self.$Utils.cloneForm(self.orderList);
				postData.pay = {
					score: {
						price: 0
					}
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res && res.solely_code == 100000) {
						self.$Utils.showToast('领取成功', 'none')
						setTimeout(function() {
							self.getUserCouponData()
						}, 1000);
					} else {
						self.$Utils.showToast(res.msg, 'none')
					}
				};
				self.$apis.couponAdd(postData, callback);
			},
			
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