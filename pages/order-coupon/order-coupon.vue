<template>
	<view>
		
		<view class="p-3">
			<view class="mb-3 p-r" v-if="userCoponData.length>0" v-for="(item,index) in userCoponData" :key="index">
				<image src="../../static/images/coupons-img.png" mode="widthFix"></image>
				<view class="flex1 p-aXY p-3 pb-4">
					<view class="font-26 colorR font-w pl-5">￥ <text class="font-70">{{item.value}}</text></view>
					<view class="color77 font-20 line-h flex-1 pl-4">
						<view class="font-28 pb-2">{{item.title}}</view>
						<view class="pb-2">有效期至：{{Utils.timeto(item.invalid_time,'ymd')}}</view>
						<view>满{{item.condition}}元使用</view>
					</view>
					<view class="p-r" @click="choose(index)">
						<!-- <image src="../../static/images/coupons-icon.png" class="wh50 mr-3"></image> -->
						<image :src="item.id==id?'../../static/images/coupons-icon.png':'../../static/images/coupons-icon1.png'" class="wh50 mr-3"></image>
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
				searchItem:{
					use_step:1
				},
				userCoponData:[],
				id:'',
				Utils:this.$Utils
			}
		},
		onLoad(options) {
			const self = this;
			self.id = uni.getStorageSync('chooseCoupon');
			self.$Utils.loadAll(['getUserCouponData'], self);
		},
		methods: {
			
			choose(index){
				const self = this;
				uni.setStorageSync('chooseCoupon',self.userCoponData[index].id);
				uni.navigateBack({
					delta:1
				})
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
			
		}
	}
</script>

<style scoped>
.font-70{font-size: 70rpx;}
.color77{color: #775312;}

.bky{width: 106rpx;height: 81rpx;}
</style>
