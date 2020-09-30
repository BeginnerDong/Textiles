<template>
	<view>
		
		<view class="mx-5 mt-5 p-3 h233 line-h p-r bB-f5">
			<image src="../../static/images/integra-img.png" mode="widthFix" class="p-aX top-0"></image>
			<view class="p-r">
				<view class="font-24 pt-3 pb-2">积分</view>
				<view class="font-80 font-w">{{userInfoData.score?userInfoData.score:0}}</view>
			</view>
		</view>
		
		<view class="flex1 py-2 bB-f5 p-r z10">
			<view class="flex0 w-50 p-r jf"
			@click="Router.navigateTo({route:{path:'/pages/integralShop/integralShop'}})">
				<image src="../../static/images/integra-icon.png" class="wh28 mr-1"></image>
				<view>积分商城</view>
			</view>
			<view class="flex0 w-50"
			@click="Router.navigateTo({route:{path:'/pages/user-integralExchange/user-integralExchange'}})">
				<image src="../../static/images/integra-icon1.png" class="wh28 mr-1"></image>
				<view>兑换记录</view>
			</view>
		</view>
		
		<view class="flex0 py-3">
			<image src="../../static/images/coupons-icon8.png" class="line"></image>
			<view class="px-2 color8">积分明细</view>
			<image src="../../static/images/coupons-icon7.png" class="line"></image>
		</view>
		
		<view class="px-3">
			<view class="flex1"  v-for="(item,index) in mainData" :key="index">
				<image v-if="item.count>0" src="../../static/images/integra-icon2.png" class="wh80"></image>
				<image v-else src="../../static/images/integra-icon3.png" class="wh80"></image>
				<view class="flex-1 py-3 bB-f5 flex1 ml-2 line-h">
					<view>
						<view>{{item.trade_info}}</view>
						<view class="font-24 color9 pt-2">{{item.create_time}}</view>
					</view>
					<view class="colorR font-32 font-w">{{item.count}}</view>
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
				userInfoData:{},
				mainData:[],
				searchItem:{
					thirdapp_id:2,
					type:3,
					count:['not in',[0]]
				}
			}
		},
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData','getUserInfoData'], self);
		},
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		methods: {
			
			getUserInfoData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userInfoData = res.info.data[0]
						self.userInfoData.score = parseInt(self.userInfoData.score)
					}
					self.$Utils.finishFunc('getUserInfoData');
				};
				self.$apis.userInfoGet(postData, callback);
			},
			
			getMainData(isNew) {
				const self = this;
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						pagesize: 10,
						is_page: true,
					}
				};
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
						for (var i = 0; i < self.mainData.length; i++) {
							self.mainData[i].score = parseInt(self.mainData[i].score)
						}
					}
					self.$Utils.finishFunc('getMainData');
			
				};
				self.$apis.flowLogGet(postData, callback);
			},
			
		}
	}
</script>

<style scoped>
.h233{height: 233rpx;}
.font-80{font-size: 80rpx;}
</style>
