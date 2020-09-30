<template>
	<view>
		
		<view v-for="(item,index) in mainData" :key="index">
			<view class="flex1 px-3 py-4 p-r line-h">
				<view class="addressTxt">
					<view class="font-30 font-w avoidOverflow">{{item.address}}</view>
					<view class="font-26 color6 pt-3">{{item.title}} <text class="pl-4">{{item.phone}}</text></view>
				</view>
				<image @click="choose(index)" :src="id==item.id?'../../static/images/shopping-icon.png':'../../static/images/shopping-icon1.png'" class="wh36"></image>
				<!-- <image src="../../static/images/shopping-icon1.png" class="wh36"></image> -->
			</view>
			<view class="f720"></view>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mainData:[],
				id:0
			}
		},
		
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getLocation'], self);
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
			
			choose(index){
				const self = this;
				self.id = self.mainData[index].id;
				uni.setStorageSync('shopData',self.mainData[index]);
				uni.navigateBack({
					delta:1
				})
			},
			
			getLocation() {
				const self = this;
				const callback = (res) => {
					if (res) {
						if (res.authSetting) {
							self.$Utils.showToast('请至小程序设置中打开位置权限，以便我们提供更好的服务')
							return
						};
						self.district = res.ad_info.district;
						self.lat = res.location.lat;
						self.lng = res.location.lng
						//self.city = res.address_component.city;
						//self.province = res.address_component.province.substring(0, res.address_component.province.length - 1);
						self.getMainData()
					}
					console.log('res', res)
					//self.$Utils.finishFunc('getLocation');
				};
				self.$Utils.getLocation('reverseGeocoder', callback);
			},
			
			getMainData(isNew) {
				const self = this;
				if(isNew){
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage:1,
						pagesize:10,
						is_page:true,
					}
				};
				const postData = {};
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = {
					menu_id:2,
					thirdapp_id:2
				};
				postData.order = {
					distance:'asc',
					longitude:self.lng,
					latitude:self.lat,
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
						for (var i = 0; i < self.mainData.length; i++) {
							self.mainData[i].distance = self.$Utils.computeDistance(self.lat,self.lng,self.mainData[i].latitude,self.mainData[i].longitude)
						}
					} else {
						self.$Utils.showToast('没有更多了', 'none');
					};
					self.$Utils.finishFunc('getLocation');
				};
				self.$apis.articleGet(postData, callback);
			},
			
		}
	}
</script>


<style scoped>
.addressTxt{width: 630rpx;}
</style>
