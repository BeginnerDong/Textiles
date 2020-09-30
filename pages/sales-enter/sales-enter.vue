<template>
	<view>
		
		<view class="info p-3 colorf">
			<view class="text-right font-26" @click="loginOff">退出</view>
			<view class="flex4">
				<image :src="userData.headImgUrl?userData.headImgUrl:''" style="overflow: hidden;border-radius: 50%;" class="wh130"></image>
				<view class="font-30 pt-3 pb-2 line-h font-w">{{userData.nickname?userData.nickname:''}}</view>
				<view class="font-20 color6 bg-f5 radius10 p-1 line-h ">{{salesData.shopInfo&&salesData.shopInfo[0]?salesData.shopInfo[0].title:''}}</view>
			</view>
			<view class="flex1 font-22 line-h pt-4 pb-2">
				<view class="flex4 w-50"
				@click="Router.navigateTo({route:{path:'/pages/sales-qrcode/sales-qrcode'}})">
					<image src="../../static/images/thesalesman-icon.png" class="wh40 mb-2"></image>
					<view>推广二维码</view>
				</view>
				<view class="flex4 w-50"
				@click="Router.navigateTo({route:{path:'/pages/sales-user/sales-user'}})">
					<view class="wh40 mb-2 font-48 font-w">{{salesData.distri?salesData.distri.length:0}}</view>
					<view>推广用户</view>
				</view>
			</view>
		</view>
		
		<view class="list mb-2">
			<view class="li" :class="liCurr==0?'on':''" @click="changeLi(0)">全部</view>
			<view class="li" :class="liCurr==1?'on':''" @click="changeLi(1)">待核销</view>
			<view class="li" :class="liCurr==2?'on':''" @click="changeLi(2)">已核销</view>
		</view>
		
		<view class="font-24 bg-white p-3" v-for="(item,index) in mainData" :key="index"
		@click="Router.navigateTo({route:{path:'/pages/orderDetail/orderDetail'}})">
			<view class="flex1">
				<!-- <image src="../../static/images/theorder-icon.png" class="wh28"></image> -->
				<image :src="item.type==1?'../../static/images/theorder-icon1.png':'../../static/images/theorder-icon.png'" class="wh28"></image>
				<view class="flex-1 pl-1">{{item.create_time}}</view>
				<view class="colorR"  v-if="item.pay_status==1&&item.transport_status==0">待核销</view>
				
				<view class="colorR" v-if="item.pay_status==1&&item.transport_status==2">已核销</view>
			</view>
			<view class="pt-3 flex1">
				<view class="flex" v-if="item.type==1">
						<image v-for="(c_item,c_index) in item.child" 
				:key="c_index" :src="c_item.orderItem&&c_item.orderItem[0]&&c_item.orderItem[0].snap_product&&c_item.orderItem[0].snap_product.product&&
									c_item.orderItem[0].snap_product.product.mainImg&&c_item.orderItem[0].snap_product.product.mainImg[0]?c_item.orderItem[0].snap_product.product.mainImg[0].url:''" class="wh160"></image>
					</view>
					
					<view class="flex" v-if="item.type==2">
							<image v-for="(c_item,c_index) in item.child" 
					:key="c_index" :src="c_item.orderItem&&c_item.orderItem[0]&&c_item.orderItem[0].snap_product&&
							c_item.orderItem[0].snap_product.mainImg&&c_item.orderItem[0].snap_product.mainImg[0]?c_item.orderItem[0].snap_product.mainImg[0].url:''" class="wh160"></image>
						</view>
				<view class="line-h text-right">
					<view class="font-32 font-w price1" v-if="item.type==1">{{item.price?item.price:''}}</view>
					<view class="font-32 font-w" v-if="item.type==2">{{item.price?item.price:''}}<span class="font-22 font-w">积分</span></view>
					<view class="color8 pt-2">共{{item.child&&item.child.length?item.child.length:''}}件</view>
				</view>
			</view>
		</view>
		
		<image src="../../static/images/thesalesman-icon1.png" class="wh100 p-f right-0"
		@click="scanCode"></image>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				liCurr:0,
				userData:{},
				salesData:{},
				mainData:[],
				searchItem:{
					pay_status:1,
					user_type:0
				}
			}
		},
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getSalesData','getUserData'], self);
		},
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		
		onShow() {
			const self = this;
			if(uni.getStorageSync('hasHx')){
				self.getMainData(true)
				uni.removeStorageSync('hasHx')
			}
		},
		
		methods: {
			
			loginOff(){
				const self = this;
				uni.removeStorageSync('sales_info');
				uni.removeStorageSync('sales_token');
				self.Router.redirectTo({route:{path:'/pages/user/user'}})
			},
			
			scanCode(){
				const self = this;
				uni.scanCode({
				    success: function (res) {
				        self.getOrderData(res.result)
				    }
				});
			},
			
			getOrderData(id) {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getSalesToken';
				postData.searchItem = {
					id:id,
					user_type:0,
					shop:self.salesData.shop
				};
				
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.Router.navigateTo({route:{path:'/pages/sales-hxOrder/sales-hxOrder?id='+res.info.data[0].id}})
					}else{
						self.$Utils.showToast('二维码无效')
					}
				};
				self.$apis.orderGet(postData, callback);
			},
			
			changeLi(i){
				const self = this;
				if(self.liCurr!=i){
					self.liCurr = i;
					if(self.liCurr==0){
						delete self.searchItem.transport_status
					}else if(self.liCurr==1){
						self.searchItem.transport_status=0
					}else if(self.liCurr==2){
						self.searchItem.transport_status=2
					}
					self.getMainData(true)
				}			
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
					};
				};
				const postData = {};
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				postData.tokenFuncName = 'getSalesToken';
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					console.log(self.mainData)
				};
				self.$apis.orderGet(postData, callback);
			},
			
			
			getSalesData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getSalesToken';
				postData.getAfter = {
					shopInfo:{
						tableName:'Article',
						middleKey:'shop',
						key:'id',
						searchItem:{
							status:1
						},
						condition:'='
					},
					distri:{
						tableName:'Distribution',
						middleKey:'user_no',
						key:'parent_no',
						searchItem:{
							status:1
						},
						condition:'='
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.salesData = res.info.data[0];
						self.searchItem.shop = self.salesData.shop;
						self.getMainData()
					};
					self.$Utils.finishFunc('getSalesData');
				};
				self.$apis.userInfoGet(postData, callback);
			},
			
			getUserData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0];
					};
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},
			
		}
	}
</script>

<style>page{background-color: #f5f5f5;}</style>
<style scoped>
.info{background-image: linear-gradient(to bottom,#191919,#474747);}
.li{width: 33.33%;}

.wh160{margin-right: 18rpx;}
.wh160:nth-child(3n){margin-right: 0;}
.wh100{top: 67%;}
</style>
