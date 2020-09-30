<template>
	<view>
		
		<view class="px-2">
			<image src="../../static/images/thesalesman-img1.png" mode="widthFix"></image>
			
			<view class="p-aXY p-5 mx-2">
				<view class="font-26 colorf mt-2">推广用户（{{childData.length?childData.length:0}}个）</view>
				
				<view class="flex flex-wrap mt-4 " v-if="childData.length>0">
					<!-- <image src="../../static/images/thesalesman-icon3.png" class="wh70"></image> -->
					<image v-for="(item,index) in childData" :key="index" 
					:src="item.headImgUrl" class="wh70"></image>
				</view>
				<view class="flex flex-wrap mt-4 " v-if="childData.length==0">
					<view style="color: #FFFFFF;">暂无数据</view>
				</view>
			</view>
		</view>
		
		<view class="flex0 pt-3">
			<image src="../../static/images/coupons-icon8.png" class="line"></image>
			<view class="px-2 color8">交易记录</view>
			<image src="../../static/images/coupons-icon7.png" class="line"></image>
		</view>
		
		<view class="px-3">
			<view class="flex1" v-for="(item,index) in mainData" :key="index" v-if="mainData.length>0">
				<image :src="item.userInfo&&item.userInfo[0]?item.userInfo[0].headImgUrl:''" class="wh80"></image>
				<view class="flex-1 py-3 bB-f5 flex1 ml-2 line-h">
					<view>
						<view>{{item.userInfo&&item.userInfo[0]?item.userInfo[0].nickname:''}}</view>
						<view class="font-24 color9 pt-2">{{item.create_time}}</view>
					</view>
					<view class="font-32 font-w price">{{item.price}}</view>
				</view>
			</view>
			<view style="width: 100%;text-align: center;">暂无数据</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				childData:[],
				mainData:[]
			}
		},
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getChildData','getMainData'], self);
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
					};
				};
				const postData = {};
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = {
					pay_status:1,
					user_type:0
				};
				postData.getBefore = {
					distri:{
						tableName:'Distribution',
						middleKey:'user_no',
						key:'child_no',
						searchItem:{
							parent_no:['in',[uni.getStorageSync('sales_info').user_no]]
						},
						condition:'='
					}
				};
				postData.getAfter = {
					userInfo:{
						tableName:'User',
						middleKey:'user_no',
						key:'user_no',
						searchItem:{
							status:1
						},
						condition:'='
					}
				};
				postData.tokenFuncName = 'getSalesToken';
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					self.$Utils.finishFunc('getMainData');
					console.log(self.mainData)
				};
				self.$apis.orderGet(postData, callback);
			},
			
			getChildData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getSalesToken';
				postData.searchItem = {
					user_type:0
				};
				postData.getBefore = {
					distri:{
						tableName:'Distribution',
						middleKey:'user_no',
						key:'child_no',
						searchItem:{
							parent_no:['in',[uni.getStorageSync('sales_info').user_no]]
						},
						condition:'='
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.childData = res.info.data;
					};
					self.$Utils.finishFunc('getChildData');
				};
				self.$apis.userGet(postData, callback);
			},
			
		}
	}
</script>

<style scoped>
.wh70{margin-left: -20rpx;border: 1px solid #f5f5f5;border-radius: 50%;margin-bottom: 15rpx;}
.wh70:nth-child(1),.wh70:nth-child(13n){margin-left: 0;}
.price{color: #222;}
</style>
