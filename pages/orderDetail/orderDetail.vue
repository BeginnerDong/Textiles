<template>
	<view>
		<!-- 待支付 -->
		<view class="Mgb p-3 flex1 pb-5" v-if="mainData.pay_status==0">
			<view class="color59 line-h flex-1">
				<view class="font-42 color pb-3 font-w">等待支付</view>
				<view>等待买家进行支付~</view>
			</view>
			<image src="../../static/images/theorder-icon4.png" class="zfIcon"></image>
		</view>
		<!-- 待发货 -->
		<view class="Mgb p-3 flex1 pb-5" v-if="mainData.pay_status==1&&mainData.transport_status==0&&mainData.transport_type==1">
			<view class="color59 line-h flex-1">
				<view class="font-42 color pb-3 font-w">等待发货</view>
				<view>卖家将尽快为您发货，请耐心等待！</view>
			</view>
			<image src="../../static/images/theorder-icon5.png" class="fhIcon"></image>
		</view>
		<!-- 待收货 -->
		<view class="Mgb p-3 flex1 pb-5" v-if="mainData.pay_status==1&&mainData.transport_status==1&&mainData.transport_type==1">
			<view class="color59 line-h flex-1">
				<view class="font-42 color pb-3 font-w">等待收货</view>
				<view>您的包裹已寄出，请注意查收~</view>
			</view>
			<image src="../../static/images/theorder-icon7.png" class="shIcon"></image>
		</view>
		<!-- 待核销 -->
		<view class="Mgb p-3 flex1 pb-5" v-if="mainData.pay_status==1&&mainData.transport_status==0&&mainData.transport_type==2">
			<view class="color59 line-h flex-1">
				<view class="font-42 color pb-3 font-w">等待核销</view>
				<view>尽快到自提门店进行核销~</view>
			</view>
			<image src="../../static/images/theorder-icon7.png" class="shIcon"></image>
		</view>
		<!-- 已收货/已核销 -->
		<view class="Mgb p-3 flex1 pb-5" v-if="mainData.pay_status==1&&mainData.transport_status==2">
			<view class="color59 line-h flex-1">
				<view class="font-42 color pb-3 font-w" v-if="mainData.transport_type==1">买家已收货</view>
				<view class="font-42 color pb-3" v-if="mainData.transport_type==2">买家已核销</view>
				<view>合作愉快哦~</view>
			</view>
			<image src="../../static/images/theorder-icon3.png" class="shIcon1"></image>
		</view>
		
		
		<view class="bg-white radius20-T p-3 line-h d-flex a-start dz">
			<image src="../../static/images/theorder-icon2.png" class="wh28"></image>
			<view class="addressTxt flex-1 pl-2" v-if="mainData.transport_type==1">
				<view class="font-26 font-w pb-3">{{mainData.snap_address.name}} <text class="pl-4">{{mainData.snap_address.phone}}</text></view>
				<view class="font-24 color9 avoidOverflow">地址：{{mainData.snap_address.city+mainData.snap_address.detail}}</view>
			</view>
			
			<view class="addressTxt flex-1 pl-2" v-if="mainData.transport_type==2">
				<view class="font-26 font-w pb-3">{{mainData.shopInfo[0].title}} <text class="pl-4">{{mainData.shopInfo[0].phone}}</text></view>
				<view class="font-24 color9 avoidOverflow">地址：{{mainData.shopInfo[0].address}}</view>
			</view>
		</view>
		<view class="f720"></view>
		
		<view class="px-3"  v-for="(item,index) in mainData.child" 
			:key="index">
			<view class="py-3 bB-f5">
				<view class="flex1">
					<image v-if="mainData.type==1" :src="item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product&&item.orderItem[0].snap_product.product&&
						item.orderItem[0].snap_product.product.mainImg&&item.orderItem[0].snap_product.product.mainImg[0]?item.orderItem[0].snap_product.product.mainImg[0].url:''" class="wh160">
					</image>
					<image v-if="mainData.type==2" :src="item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product&&
						item.orderItem[0].snap_product.mainImg&&item.orderItem[0].snap_product.mainImg[0]?item.orderItem[0].snap_product.mainImg[0].url:''" class="wh160">
					</image>
					<view class="flex5 font-30 py-0 flex-1 pl-2 h160">
						<view class="avoidOverflow w510">{{item.product_title}}</view>
						<view class="font-24 color9 flex-1" v-if="mainData.type==1">
							<span v-for="(c_item,key,c_index) in item.orderItem[0].snap_product.label_description" :key="key">{{key}}:{{c_item}}</span>
						</view>
						<view class="flex1">
							<view class="price1 font-32 font-w" v-if="mainData.type==1">{{item.price}}</view>
							<view class="font-32 font-w" v-if="mainData.type==2">{{item.price?item.price:''}}<span class="font-22 font-w">积分</span></view>
							<view class="font-24 color8">数量：{{item.count}}</view>
						</view>
					</view>
				</view>
				<view class="flex1 pl-180 pt-2" v-if="mainData.transport_type==2">
					<view class="font-24 color9">核销码：</view>
					<image :src="mainData.qrCode" class="wh80"></image>
				</view>
			</view>
		</view>
		<view class="f720"></view>
		
		<view class="px-3 font-26">
			<view class="flex">
				<view class="color9 pr-4">订单编号：</view>
				<view class="py-3 bB-f5 flex-1">{{mainData.order_no?mainData.order_no:''}}</view>
			</view>
			<view class="flex">
				<view class="color9 pr-4">下单时间：</view>
				<view class="py-3 bB-f5 flex-1">{{mainData.create_time?mainData.create_time:''}}</view>
			</view>
			<view class="flex">
				<view class="color9 pr-4">商品数量：</view>
				<view class="py-3 bB-f5 flex-1">{{mainData.child.length?mainData.child.length:''}}</view>
			</view>
			<view class="flex">
				<view class="color9 pr-4">商品总额：</view>
				<view class="price py-3 bB-f5 flex-1">{{mainData.price?mainData.price:''}}</view>
			</view>
			<view class="flex">
				<view class="color9 pr-4">满减金额：</view>
				<view class="py-3 bB-f5 flex-1">-￥{{mainData.discount_price ?mainData.discount_price:''}}</view>
			</view>
		</view>
		<view class="p-3 text-right pb-5">
			实付款： <text class="price1 red font-36 font-w">{{mainData.actual_price?mainData.actual_price :''}}</text>
		</view>
		<view class="f720"></view>
		<view style="height: 100rpx;"></view>
		<view class="d-flex j-end p-3" style="position: fixed;bottom: 0;background-color: #fff;width: 100%;">
			<view class="btnOrder" @click="orderUpdate(1)" v-if="mainData.pay_status==0">取消订单</view>
			<view class="btnOrder order2" v-if="mainData.pay_status==0" @click="goPay">去支付</view>
			<view class="btnOrder order2"   @click="orderUpdate(2)"  v-if="mainData.pay_status==1&&mainData.transport_status==1&&mainData.type==1">确认收货</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mainData:{}
			}
		},
		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			
			goPay() {
				const self = this;	
				self.pay= self.mainData.pay;
				const postData = self.$Utils.cloneForm(self.pay);	
				postData.tokenFuncName = 'getProjectToken',
				postData.searchItem = {
					id: self.mainData.id
				};
				const callback = (res) => {
					if (res.solely_code == 100000) {
						uni.setStorageSync('canClick', true);
					
						if (res.info) {
							const payCallback = (payData) => {
								console.log('payData', payData)
								if (payData == 1) {
									self.$Utils.showToast('支付成功','none')
									setTimeout(function() {
										self.getMainData()
									}, 1000);
								} else {
									self.$Utils.showToast('支付失败','none')
								};
							};
							self.$Utils.realPay(res.info, payCallback);
						} else {
							self.$Utils.showToast('支付成功','none')
							setTimeout(function() {
								self.getMainData()
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
			
			orderUpdate(type) {
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
					id:self.mainData.id,
				};
				const callback = (data) => {
					uni.setStorageSync('canClick', true);
					if (data && data.solely_code == 100000) {
						self.$Utils.showToast('操作成功','none');
						setTimeout(function() {
							self.getMainData()
						}, 1000);
					} else {
						self.$Utils.showToast(data.msg,'none')
					}
				};
				self.$apis.orderUpdate(postData, callback);
			 },
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					id: self.id,
				};
				postData.getAfter = {
					shopInfo:{
						tableName:'Article',
						middleKey:'shop',
						key:'id',
						searchItem:{
							status:1
						},
						condition:'='
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
					};
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
			
		}
	}
</script>

<style scoped>
.color59{color: #593F12;}
.fhIcon{width: 74rpx;height: 72rpx;}
.zfIcon{width: 80rpx;height: 78rpx;}
.shIcon{width: 88rpx;height: 73rpx;}
.shIcon1{width: 74rpx;height: 74rpx;}

.dz{margin-top: -20rpx;}
.price1,.price{color: #222;}
.h160{height: 160rpx;}
.w510{width: 510rpx;}
.red{color: #EA2131;}
.pl-180{padding-left: 180rpx;}

.btnOrder{width: 130rpx;margin-left: 20rpx;}
.order2{border-color: #E6B968;color: #E6B968;}
</style>
