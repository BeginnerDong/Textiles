<template>
	<view>
		
		<view class="bg-white radius10 p-3 line-h d-flex a-start dz m-3">
			<image src="../../static/images/theorder-icon2.png" class="wh28"></image>
			<view class="addressTxt flex-1 pl-2">
				<view class="font-26 font-w pb-3">{{mainData.name?mainData.name:''}} <text class="pl-4">{{mainData.phone?mainData.phone:''}}</text></view>
				<view class="font-24 color9 avoidOverflow">地址：{{mainData.shopInfo&&mainData.shopInfo[0]?mainData.shopInfo[0].address:''}}</view>
			</view>
		</view>
		
		<view class="flex1 p-3 mt-3 mx-3 bg-white radius10" v-for="(item,index) in mainData.child" 
			:key="index">
			<image v-if="mainData.type==1" :src="item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product&&item.orderItem[0].snap_product.product&&
				item.orderItem[0].snap_product.product.mainImg&&item.orderItem[0].snap_product.product.mainImg[0]?item.orderItem[0].snap_product.product.mainImg[0].url:''" class="wh200">
			</image>
			<image v-if="mainData.type==2" :src="item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product&&
				item.orderItem[0].snap_product.mainImg&&item.orderItem[0].snap_product.mainImg[0]?item.orderItem[0].snap_product.mainImg[0].url:''" class="wh200">
			</image>
			<view class="flex5 py-0 flex-1 pl-2 h200">
				<view class="avoidOverflow2">{{item.product_title}}</view>
				
				<view class="color9 flex-1 font-24 pt-1" v-if="mainData.type==1">
					<span v-for="(c_item,key,c_index) in item.orderItem[0].snap_product.label_description" :key="key">{{key}}:{{c_item}}</span>
				</view>
				<view class="price1 font-32 font-w" v-if="mainData.type==1">{{item.price}}</view>
				<view class="font-32 font-w" v-if="mainData.type==2">{{item.price?item.price:''}}<span class="font-22 font-w">积分</span></view>
			</view>
		</view>
		
		
		<view class="bg-white px-3 py-2 bT-e1 p-fX bottom-0" @click="orderUpdate(mainData.id)">
			<view class="btn80 Mgb">确认核销</view>
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
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getSalesToken';
				postData.searchItem = {
					id: self.id,
					user_type:0
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
			
			orderUpdate(id) {
				const self = this;
				uni.setStorageSync('canClick', false);
				uni.showModal({
				    title: '提示',
				    content: '确定要核销此订单吗',
					confirmColor:'#db1b1b',
				    success: function (res) {
				        if (res.confirm) {
				            const postData = {};
				            postData.tokenFuncName = 'getSalesToken';
				            postData.data = {
								transport_status:2
							};
				            postData.searchItem = {
				            	id:id,
				            	user_type:0
				            };
				            const callback = (data) => {
				            	uni.setStorageSync('canClick', true);
				            	if (data && data.solely_code == 100000) {
				            		self.$Utils.showToast('操作成功','none');
				            		self.setStorageSync('hasHx',true)
				            		setTimeout(function() {
				            			uni.navigateBack({
				            				delta:1
				            			})
				            		}, 1000);
				            	} else {
				            		self.$Utils.showToast(data.msg,'none')
				            	}
				            };
				            self.$apis.orderUpdate(postData, callback);
				        } else if (res.cancel) {
			
				        }
				    }
				});
				
			 },
			
		}
	}
</script>
<style>page{background-image: linear-gradient(to bottom,#E6B968 ,#f5f5f5 30%);background-color: #f5f5f5;}</style>
<style scoped>
.h200{height: 200rpx;}
</style>
