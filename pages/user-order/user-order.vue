<template>
	<view>
		<!-- 快递订单 -->
		<view class="list mb-2 shadowM" v-show="type==0">
			<view class="li" :class="liCurr==0?'on':''" @click="changeLi(0)">全部</view>
			<view class="li" :class="liCurr==1?'on':''" @click="changeLi(1)">待支付</view>
			<view class="li" :class="liCurr==2?'on':''" @click="changeLi(2)">待发货</view>
			<view class="li" :class="liCurr==3?'on':''" @click="changeLi(3)">待收货</view>
			<view class="li" :class="liCurr==4?'on':''" @click="changeLi(4)">已完成</view>
		</view>
		<!-- 自提订单 -->
		<view class="list mb-2 shadowM" v-show="type==1">
			<view class="li li1" :class="liCurr==0?'on':''" @click="changeLiTwo(0)">全部</view>
			<view class="li li1" :class="liCurr==1?'on':''" @click="changeLiTwo(1)">待支付</view>
			<view class="li li1" :class="liCurr==2?'on':''" @click="changeLiTwo(2)">待核销</view>
			<view class="li li1" :class="liCurr==3?'on':''" @click="changeLiTwo(3)">已核销</view>
		</view>
		
		
		<!-- 快递订单 -->
		<view class="font-24 bg-white p-3 mb-2" v-if="type==0" v-for="(item,index) in mainData" :key="index"
		>
			<view class="flex1">
				<image :src="item.type==1?'../../static/images/theorder-icon1.png':'../../static/images/theorder-icon.png'" class="wh28"></image>
				<view class="flex-1 pl-1">{{item.create_time}}</view>
				<view class="colorR" v-if="item.pay_status==0">待支付</view>
				<view class="colorR"  v-if="item.pay_status==1&&item.transport_status==0">待发货</view>
				<view class="colorR" v-if="item.pay_status==1&&item.transport_status==1">待收货</view>
				<view class="colorR" v-if="item.pay_status==1&&item.transport_status==2">已完成</view>
			</view>
			<view class="pt-3 flex1" :data-id="item.id"
		@click="Router.navigateTo({route:{path:'/pages/orderDetail/orderDetail?id='+$event.currentTarget.dataset.id}})">
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
			<view class="d-flex j-end pt-3">
				<view class="btnOrder" v-if="item.pay_status==0" @click="orderUpdate(index,1)">取消订单</view>
				<view class="btnOrder order2" v-if="item.pay_status==0" @click="goPay(index)">去支付</view>
				<view class="btnOrder order2" v-if="item.pay_status==1&&item.transport_status==1" @click="orderUpdate(index,2)">确认收货</view>
			</view>
		</view>
		
		<!-- 自提订单 -->
		<view class="font-24 bg-white p-3 mb-2" v-if="type==1" v-for="(item,index) in mainData" :key="index"
		:data-id="item.id"
		@click="Router.navigateTo({route:{path:'/pages/orderDetail/orderDetail?id='+$event.currentTarget.dataset.id}})">
			<view class="flex1">
				<image :src="item.type==1?'../../static/images/theorder-icon1.png':'../../static/images/theorder-icon.png'" class="wh28"></image>
				<view class="flex-1 pl-1">{{item.create_time}}</view>
				<view class="colorR" v-if="item.pay_status==0">待支付</view>
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
			<view class="d-flex j-end pt-3">
				<view class="btnOrder" v-if="item.pay_status==0" @click="orderUpdate(index,1)">取消订单</view>
				<view class="btnOrder order2" v-if="item.pay_status==0" @click="goPay(index)">去支付</view>
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
				type:-1,
				mainData:[],
				searchItem:{
					level:1,
					
				},
			}
		},
		onLoad(options){
			const self = this;
			self.type = options.type;
			self.searchItem.transport_type = parseInt(self.type)+1
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
			
			goPay(index) {
				const self = this;	
				self.pay= self.mainData[index].pay;
				const postData = {
					wxPay:{
						price:self.mainData[index].price
					}
				};	
				postData.tokenFuncName = 'getProjectToken',
				postData.searchItem = {
					id: self.mainData[index].id
				};
				console.log('postData',postData)
				//return
				const callback = (res) => {
					if (res.solely_code == 100000) {
						uni.setStorageSync('canClick', true);
					
						if (res.info) {
							const payCallback = (payData) => {
								console.log('payData', payData)
								if (payData == 1) {
									self.$Utils.showToast('支付成功','none')
									setTimeout(function() {
										self.getMainData(true)
									}, 1000);
								} else {
									self.$Utils.showToast('支付失败','none')
								};
							};
							self.$Utils.realPay(res.info, payCallback);
						} else {
							self.$Utils.showToast('支付成功','none')
							setTimeout(function() {
								self.getMainData(true)
							}, 1000);
						};
					} else {
						uni.setStorageSync('canClick', true);
						uni.showToast({
							title: res.msg,
							duration: 2000
						});
					};
				};
				self.$apis.pay(postData, callback);
			},
			
			orderUpdate(index,type) {
				const self = this;
				uni.setStorageSync('canClick', false);
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.data = {
					
				};
				if(type==1){
					postData.data.status=-1
				}else{
					postData.data.transport_status=2
				};
				postData.searchItem = {
					id:self.mainData[index].id,
				};
				const callback = (data) => {
					uni.setStorageSync('canClick', true);
					if (data && data.solely_code == 100000) {
						self.$Utils.showToast('操作成功','none');
						setTimeout(function() {
							self.getMainData(true)
						}, 1000);
					} else {
						self.$Utils.showToast(data.msg,'none')
					}
				};
				self.$apis.orderUpdate(postData, callback);
			 },
			
			changeLi(i){
				const self = this;
				if(self.liCurr!=i){
					self.liCurr = i;
					if(self.liCurr==0){
						delete self.searchItem.transport_status
						delete self.searchItem.pay_status
					}else if(self.liCurr==1){
						self.searchItem.pay_status=0;
						delete self.searchItem.transport_status
					}else if(self.liCurr==2){
						self.searchItem.pay_status=1;
						self.searchItem.transport_status=0
					}else if(self.liCurr==3){
						self.searchItem.pay_status=1;
						self.searchItem.transport_status=1
					}else if(self.liCurr==4){
						self.searchItem.pay_status=1;
						self.searchItem.transport_status=2
					}
					self.getMainData(true)
				}			
			},
			
			changeLiTwo(i){
				const self = this;
				if(self.liCurr!=i){
					self.liCurr = i;
					if(self.liCurr==0){
						delete self.searchItem.transport_status
						delete self.searchItem.pay_status
					}else if(self.liCurr==1){
						self.searchItem.pay_status=0;
						delete self.searchItem.transport_status
					}else if(self.liCurr==2){
						self.searchItem.pay_status=1;
						self.searchItem.transport_status=0
					}else if(self.liCurr==3){
						self.searchItem.pay_status=1;
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
						is_page: true,
						pagesize: 10
					}
				};
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				postData.searchItem.user_no = uni.getStorageSync('user_info').user_no;
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
		}
	}
</script>
<style>page{background-color: #f7f7f7;}</style>
<style scoped>
.li{width: 20%;}
.li1{width: 25%;}
.wh160{margin-right: 15rpx;}
.wh160:nth-child(3n){margin-right: 0;}
.price1{color: #222;}

.btnOrder{width: 130rpx;margin-left: 20rpx;}
.order2{border-color: #E6B968;color: #E6B968;}
</style>
