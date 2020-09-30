<template>
	<view class="px-3">
		
		<view class="flex1" v-for="(item,index) in mainData" :key="index">
			<image src="../../static/images/integra-icon3.png" class="wh80"></image>
			<view class="flex-1 py-3 bB-f5 flex1 ml-2 line-h">
				<view>
					<view>积分兑换商品</view>
					<view class="font-24 color9 pt-2">{{item.create_time}}</view>
				</view>
				<view class="font-32 font-w">{{item.count}}</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mainData:[],
				searchItem:{
					thirdapp_id:2,
					type:3,
					count:['<',0]
				}
			}
		},
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData'], self);
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

<style>

</style>
