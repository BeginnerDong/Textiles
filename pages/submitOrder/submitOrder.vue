<template>
	<view>
		
		<view class="m-3 bg-white radius10 color2 line-h p-r">
			<image src="../../static/images/submit-img.png" mode="widthFix" class="bgAdd"
			v-show="tabCurr==0"></image>
			<image src="../../static/images/submit-img2.png" mode="widthFix" class="bgAdd"
			v-show="tabCurr==1"></image>
			<view class="flex text-center font-30 radius10 p-r line-h pt-1">
				<view class="w-50 pb-3 pt-1" @click="changeTab(0)">快递配送</view>
				<view class="w-50 pb-3 pt-1" @click="changeTab(1)">到店自提</view>
			</view>
			<view  v-show="tabCurr==0">
				<view class="flex1 px-3 py-4 p-r"
				@click="Router.navigateTo({route:{path:'/pages/address/address'}})">
					<view class="addressTxt" v-if="addressData.name">
						<view class="font-30 font-w avoidOverflow">{{addressData.city+addressData.detail}}</view>
						<view class="font-26 color9 pt-3">{{addressData.name}} <text class="pl-4">{{addressData.phone}}</text></view>
					</view>
					<view class="addressTxt"  v-else>
						<view class="">选择收货地址</view>
					</view>
					<image src="../../static/images/details-icon2.png" class="jt-icon"></image>
				</view>
			</view>
			<view  v-show="tabCurr==1">
				<view class="flex1 px-3 py-4 p-r"
				@click="Router.navigateTo({route:{path:'/pages/selfRaising/selfRaising'}})">
					<view class="addressTxt" v-if="shopData.address">
						<view class="font-30 font-w avoidOverflow">{{shopData.address}}</view>
						<view class="font-26 color9 pt-3">{{shopData.title}} <text class="pl-4">{{shopData.phone}}</text></view>
					</view>
					<view class="addressTxt"  v-else>
						<view class="">选择自提点</view>
					</view>
					<image src="../../static/images/details-icon2.png" class="jt-icon"></image>
				</view>
				<view class="flex1 py-3 mx-3 bT-f5 p-r">
					<input type="text" v-model="orderInfo.name" placeholder="收货人姓名" />
					<input type="text" v-model="orderInfo.phone" placeholder="电话" />
				</view>
			</view>
		</view>
		
		<view class="bg-white p-3 mx-3 radius10" v-if="type==1" v-for="(item,index) in mainData" :key="index">
			<view class="flex1 pb-3 bB-f5 w750 flex-shrink">
				<image :src="item.product&&item.product.mainImg&&item.product.mainImg[0]?item.product.mainImg[0].url:''" class="wh200"></image>
				<view class="flex5 font-30 py-0 flex-1 pl-2 h200">
					<view class="avoidOverflow2">{{item.product&&item.product.title?item.product.title:''}}</view>
					<view class="font-24 color9 flex-1 line-h pt-1">
							<span v-for="(c_item,key,c_index) in item.product.sku[item.skuIndex].label_description" :key="key">{{key}}:{{c_item}}</span>
					</view>
					<view class="price1 font-32 font-w">{{item.product&&item.product.sku&&item.product.sku[item.skuIndex]?item.product.sku[item.skuIndex].price:''}}</view>    <!-- 正常订单 -->
				</view>
			</view>
			<view class="flex1 pt-3">
				<view class="color8">购买数量</view>
				<view class="count">
					<view class="countIcon"  @click="counter(index,'-')"><image src="../../static/images/shopping-icon4.png" class="countIcon1"></image></view>
					<view class="countNum">{{item.count}}</view>
					<view class="countIcon" @click="counter(index,'+')"><image src="../../static/images/shopping-icon3.png" class="countIcon2"></image></view>
				</view>
			</view>
		</view>
		
		<view class="bg-white p-3 mx-3 radius10" v-if="type==2" v-for="(item,index) in mainData" :key="index">
			<view class="flex1 pb-3 bB-f5 w750 flex-shrink">
				<image :src="item.product&&item.product.mainImg&&item.product.mainImg[0]?item.product.mainImg[0].url:''" class="wh200"></image>
				<view class="flex5 font-30 py-0 flex-1 pl-2 h200">
					<view class="avoidOverflow2">{{item.product&&item.product.title?item.product.title:''}}</view>
					<view class="font-32 font-w colorR">{{item.product&&item.product.price?item.product.price:''}}<text class="font-22">积分</text></view>      <!-- 积分订单 -->
				</view>
			</view>
		</view>
		
		<view class="bg-white px-3 mx-3 mt-2 radius10 line-h" v-if="type==1">
			<!-- 普通订单展示优惠券 -->
			<view class="flex1 py-4 bB-f5"
			@click="Router.navigateTo({route:{path:'/pages/order-coupon/order-coupon'}})">
				<view class="color8">优惠券</view>
				<view class="flex">
					<view>{{couponData.id?'满'+couponData.condition+'减'+couponData.value:'请选择优惠劵'}}</view>
					<image src="../../static/images/details-icon2.png" class="jt-icon ml-1"></image>
				</view>
			</view>
			<!-- <view class="flex1 py-4">
				<view class="color8">运费</view>
				<view>￥10</view>
			</view> -->
		</view>
		
		<view class="bg-white bT-e1 flex1 p-fX bottom-0">
			<view class="font-22 color9 px-3">合计：
				<text class="font-32 price1 font-w" v-if="type==1">{{totalPrice}}</text>
				<text class="font-32 font-w colorR" v-if="type==2">{{totalPrice}}<text class="font-22">积分</text></text>
			</view>
			<view class="w230 Mgb font-30 z100"  v-if="type==1" @click="Utils.stopMultiClick(submit)">提交订单</view>
			<view class="w230 Mgb font-30" v-if="type==2" @click="Utils.stopMultiClick(submit)">立即兑换</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				tabCurr:0,
				type:0,
				totalPrice:0,
				payType:1,
				pay:{
					coupon:[]
				},
				payScore:{},
				mainData:[],
				Utils:this.$Utils,
				orderInfo:{
					name:'',
					phone:''
				},
				addressData:{},
				shopData:{},
				couponData:{}
			}
		},
		onLoad(options) {
			const self = this;
			uni.removeStorageSync('chooseCoupon');
			uni.setStorageSync('canClick', true);
			self.mainData = uni.getStorageSync('payPro');
			console.log('self.mainData',self.mainData)
			self.type = self.mainData[0].type;
			console.log('self.type',self.type)
			if(self.type==1){
				self.countTotalPrice()
			}else{
				self.countTotalScore()
			}
		},
		
		onShow() {
			const self = this;
			if(uni.getStorageSync('choosedAddressData')){
				self.addressData = uni.getStorageSync('choosedAddressData')
			}else{
				self.getAddressData()
			};
			if(uni.getStorageSync('shopData')){
				self.shopData = uni.getStorageSync('shopData')
			}
			if(uni.getStorageSync('chooseCoupon')){
				
				self.getUserCouponData()
			}
		},
		
		methods: {
			
			getUserCouponData() {
				const self = this;
				var now = Date.parse(new Date());
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					id: uni.getStorageSync('chooseCoupon'),
					//pay_status:1,
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.couponData = res.info.data[0]
						self.useCoupon()
					}
				};
				self.$apis.userCouponGet(postData, callback);
			},
			
			useCoupon() {
				const self = this;	
				self.couponTotalPrice = self.$Utils.addItemInArray(self.pay.coupon, 'price');
			/* 	console.log(index)
				console.log(self.couponData);
				console.log(self.couponData[0]); */
				/* for (var i = 0; i < self.mainData.length; i++) {
					self.totalPrice += parseFloat(parseFloat(self.mainData[i].product.sku[self.mainData[i].skuIndex].price)*parseFloat(self.mainData[i].count)).toFixed(2)
				}; */
				console.log('self.totalPrice', self.totalPrice)
				if(self.couponData.id){
					var id = self.couponData.id;
				}else{
					self.pay.coupon = []
					self.countTotalPrice();
					console.log('self.pay',self.pay)
					return
				}
				
				var findCoupon = self.couponData;
				var findItem = self.$Utils.findItemInArray(self.pay.coupon, 'id', id);
				/* if (findCoupon) {
					findCoupon = findCoupon[1];
					var findSameCoupon =  self.$Utils.findItemsInArray(self.pay.coupon, 'product_id', id);
				} else {
					self.$Utils.showToast('优惠券错误', 'none');
					return;
				}; */
				if (findItem) {
					self.countTotalPrice();
					console.log('self.pay',self.pay)
					return
				} else {
					console.log('self.totalPrice', self.totalPrice)
					console.log('self.totalPrice', self.couponTotalPrice)
					console.log('self.totalPrice', findCoupon.condition)
					if ((self.totalPrice - self.couponTotalPrice) < findCoupon.condition) {
						self.$Utils.showToast('未达满减标准', 'none');	
						self.couponData = {};
						return;
					};			
					self.pay = {
						coupon:[]
					};
					//console.log('findSameCoupon.length', findSameCoupon.length)
					if (self.pay.coupon.length >= 1) {
						self.$Utils.showToast('叠加使用超限', 'none');
					
						return;
					};
					
					if (findCoupon.type == 1) {
						var couponPrice = findCoupon.value;
						console.log('findCoupon.discount', findCoupon.discount)
					} else if (findCoupon.type == 2) {
						
						var couponPrice = parseFloat(self.totalPrice).toFixed(2) - parseFloat(findCoupon.discount / 100 * self.totalPrice)
							.toFixed(2);
					};
					/* if (parseFloat(couponPrice) + parseFloat(self.couponTotalPrice) > parseFloat(self.totalPrice)) {
						couponPrice = parseFloat(self.totalPrice).toFixed(2) - parseFloat(self.couponTotalPrice).toFixed(2);
					}; */
					self.pay.coupon.push({
						id: id,
						price: couponPrice.toFixed(2),
					});
				};
				self.countTotalPrice();
			},
			
			test(){
				console.log(222)
			},
			
			counter(index, type) {
				const self = this;
				if (type == '+') {
					self.mainData[index].count++;
				} else {
					if (self.mainData[index].count > 1) {
						self.mainData[index].count--;
					}
				};
				self.countTotalPrice();
			},
			
			
			countTotalPrice() {
				const self = this;
				self.totalPrice = 0;
				self.couponTotalPrice = self.$Utils.addItemInArray(self.pay.coupon, 'price');
				for (var i = 0; i < self.mainData.length; i++) {
					self.totalPrice += self.mainData[i].product.sku[self.mainData[i].skuIndex].price*self.mainData[i].count
				}
				self.totalPrice = (parseFloat(self.totalPrice) - parseFloat(self.couponTotalPrice)).toFixed(2)
				//console.log('wxPay',wxPay)
				if (self.totalPrice > 0) {
					self.pay.wxPay = {
						price: self.totalPrice,
					};
				} else {
					  delete self.pay.wxPay;	 
				};
				console.log(self.pay)
			},
			
			countTotalScore() {
				const self = this;
				self.totalPrice = 0;
				for (var i = 0; i < self.mainData.length; i++) {
					self.totalPrice += self.mainData[i].product.price*self.mainData[i].count
				}
				self.totalPrice = (parseFloat(self.totalPrice)).toFixed(2)
				//console.log('wxPay',wxPay)
				if (self.totalPrice > 0) {
					self.payScore.score = {
						price: self.totalPrice,
					};
				} else {
					  delete self.payScore.score;	 
				};
				console.log(self.payScore)
			},
			
			getAddressData() {
				const self = this;		
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					isdefault:1
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.addressData = res.info.data[0];
					}
				};
				self.$apis.addressGet(postData, callback);
			},
			
			changeTab(i){
				const self = this;
				self.tabCurr = i
			},
			
			//type==1提交
			submit(){
				const self = this;
				console.log(1234)
				uni.setStorageSync('canClick', false);
				if(self.tabCurr==1){
					if (JSON.stringify(self.shopData) == '{}') {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('请选择自提门店', 'none', 1000)
						return;
					}
					if(self.orderInfo.name==''||self.orderInfo.phone==''){
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('请填写提货人信息','none')
						return
					}
					if (self.orderInfo.phone.trim().length != 11 || !/^1[3|4|5|6|7|8|9]\d{9}$/.test(self.orderInfo.phone)) {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('请输入正确的手机号', 'none', 1000)
						return;
					}
				}else{
					if(JSON.stringify(self.addressData) == '{}'){
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('请选择收货地址','none')
						return
					}
				};
				var orderList = []
				/* for (var i = 0; i < self.mainData.length; i++) {
					orderList.push({product_id:self.mainData[i].product_id,count:self.mainData[i].count,type:self.mainData[i].type})
				} */
				if(self.type==1){
					var data = {};
					for (var i = 0; i < self.mainData.length; i++) {
						orderList.push({sku_id:self.mainData[i].sku_id,count:self.mainData[i].count})
					}
					self.addOrder(orderList)
				}else{
					var data = {};
					for (var i = 0; i < self.mainData.length; i++) {
						orderList.push({product_id:self.mainData[i].product_id,count:self.mainData[i].count})
					}
					self.addScoreOrder(orderList)
				}
				
			},
			
			addOrder(orderList) {
				const self = this;	
				
				/* if(self.orderId){
					self.goPay()
					return
				}; */
				const postData = {}; 
				postData.orderList = self.$Utils.cloneForm(orderList);
				postData.data = {
					type:1,
					level:1,
					price:self.pay.wxPay.price,
					actual_price:self.pay.wxPay.price,
					discount_price:self.$Utils.addItemInArray(self.pay.coupon, 'price'),
					transport_type:self.tabCurr+1,
					pay:self.pay
				};
				postData.type = 1;
				postData.tokenFuncName = 'getProjectToken';
				if(self.tabCurr==0){
					postData.data.snap_address = self.addressData
				}else{
					postData.data.name = self.orderInfo.name
					postData.data.phone = self.orderInfo.phone
					postData.data.shop = self.shopData.id
				};
				const callback = (res) => {
					uni.setStorageSync('canClick', true);
					if (res && res.solely_code == 100000) {
						self.orderId = res.info.id;
						var array = self.$Utils.getStorageArray('cartData');
						for (var i = 0; i < orderList.length; i++) {
							for (var j = 0; j < array.length; j++) {
								if(orderList[i].sku_id == array[j].sku[array[j].skuIndex].id){
									self.$Utils.delStorageArray('cartData', orderList[i], 'id');
								}
							}
						};
						self.goPay()
					} else {		
						uni.showToast({
							title: res.msg,
							duration: 2000
						});
					};		
				};
				self.$apis.addOrder(postData, callback);
			},
			
			addScoreOrder(orderList) {
				const self = this;	
				
				/* if(self.orderId){
					self.goPay()
					return
				}; */
				const postData = {}; 
				postData.orderList = self.$Utils.cloneForm(orderList);
				postData.data = {
					type:2,
					level:1,
					price:self.payScore.score.price,
					actual_price:self.payScore.score.price,
					transport_type:self.tabCurr+1,
					pay:self.pay
				};
				postData.type = 2;
				postData.tokenFuncName = 'getProjectToken';
				if(self.tabCurr==0){
					postData.data.snap_address = self.addressData
				}else{
					postData.data.name = self.orderInfo.name
					postData.data.phone = self.orderInfo.phone
					postData.data.shop = self.shopData.id
				};
				const callback = (res) => {
					uni.setStorageSync('canClick', true);
					if (res && res.solely_code == 100000) {
						self.orderId = res.info.id;
						self.goScorePay()
					} else {		
						uni.showToast({
							title: res.msg,
							duration: 2000
						});
					};		
				};
				self.$apis.addOrder(postData, callback);
			},
			
			goPay() {
				const self = this;	
				const postData = self.$Utils.cloneForm(self.pay);	
				postData.tokenFuncName = 'getProjectToken',
				postData.searchItem = {
					id: self.orderId
				};
				postData.payAfter = [];
				postData.payAfter.push({
					tableName: 'FlowLog',
					FuncName: 'add',
					data: {
						type:3,
						count:100,
						trade_info:'完成订单',
						account:1,
						thirdapp_id:2,
						user_no:uni.getStorageSync('user_info').user_no
					},
				});
				const callback = (res) => {
					if (res.solely_code == 100000) {
						uni.setStorageSync('canClick', true);
					
						if (res.info) {
							const payCallback = (payData) => {
								console.log('payData', payData)
								if (payData == 1) {
									self.$Utils.showToast('支付成功','none')
									setTimeout(function() {
										self.$Router.redirectTo({route:{path:'/pages/user-order/user-order?type='+self.tabCurr}})
									}, 1000);
								} else {
									uni.setStorageSync('canClick', true);
									self.$Utils.showToast('支付失败','none')
								};
							};
							self.$Utils.realPay(res.info, payCallback);
						} else {
							
							self.$Utils.showToast('支付成功','none')
							setTimeout(function() {
								self.$Router.redirectTo({route:{path:'/pages/user-order/user-order?type='+self.tabCurr}})
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
			
			goScorePay() {
				const self = this;	
				const postData = self.$Utils.cloneForm(self.payScore);	
				postData.tokenFuncName = 'getProjectToken',
				postData.searchItem = {
					id: self.orderId
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
										self.$Router.redirectTo({route:{path:'/pages/user-order/user-order?type='+self.tabCurr}})
									}, 1000);
								} else {
									uni.setStorageSync('canClick', true);
									self.$Utils.showToast('支付失败','none')
								};
							};
							self.$Utils.realPay(res.info, payCallback);
						} else {
							self.$Utils.showToast('支付成功','none')
							setTimeout(function() {
								self.$Router.redirectTo({route:{path:'/pages/user-order/user-order?type='+self.tabCurr}})
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
		}
	}
</script>

<style>
page{background-image: linear-gradient(to bottom, #E6B968, #f5f5f5 40%);background-color: #f5f5f5;}
</style>
<style scoped>
.addressTxt{width: 530rpx;}
.bgAdd{position: absolute;top: 0;margin-top: -10rpx;}
.h200{height: 200rpx;}
.w230{width: 230rpx;line-height: 100rpx;text-align: center;}
input{width: 300rpx;height: 60rpx;text-align: center;font-size: 24rpx;border-radius: 10rpx;border: 1px solid #e1e1e1;}
</style>
