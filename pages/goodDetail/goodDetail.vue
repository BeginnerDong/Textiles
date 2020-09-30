<template>
	<view v-if="showAll">
		<!-- 轮播 -->
		<swiper class="swiper-box" indicator-dots="indicatorDots" autoplay="autoplay" interval="3000" indicator-active-color="#E6B968">
			<block>
				<swiper-item class="swiper-item" v-for="(item,index) in mainData.bannerImg" :key="index">
					<image :src="item.url" />
				</swiper-item>
			</block>
		</swiper>
		
		<!-- 详情 -->
		<view class="p-3 flex1">
			<view class="price1 colorR font-40" v-if="mainData.type==1">{{mainData.sku[specsCurr]?mainData.sku[specsCurr].price:''}}</view>
			<view class="colorR font-40" v-if="mainData.type==2">{{mainData.price}} <text class="font-22">积分</text></view>      <!-- 积分商品展示 -->
			<button class="flex4 font-22" v-if="mainData.type==1" open-type="share">        <!-- 积分商品不展示分享 -->
				<image src="../../static/images/details-icon.png" class="wh30 mb-2"></image>
				<view>分享</view>
			</button>
		</view>
		<view class="font-32 font-w color2 mx-3 pb-3 bB-f5">{{mainData.title}}</view>
		<view class="flex p-3 line-h">
			<view class="color8 pr-5">配送</view>
			<view class="flex1 pr-3">
				<image src="../../static/images/details-icon1.png" class="wh20 mr-1"></image>
				<view>快递配送</view>
			</view>
			<view class="flex1">
				<image src="../../static/images/details-icon1.png" class="wh20 mr-1"></image>
				<view>到店自提</view>
			</view>
		</view>
		<view class="f8-16"></view>
		
		<view class="flex p-3 line-h" v-if="mainData.type==1" @click="ggShow">
			<view class="color8 pr-5">规格</view>
			<view class="flex-1 pr-3" v-if="specsCurr>=0">已选
				<span v-for="(item,index) in labelData" :key="index">
					{{item.title}}:
					<span v-for="(c_item,c_index) in item.children" :key="c_item.id" 
						v-show = "Utils.inArray(c_item.id,sku_item)!=-1"
						class="mr-2"
					>{{c_item.title}}</span>
				</span>
				<span class="ml-2">*{{count}}</span>
			</view>
			<view class="flex-1 pr-3" v-if="specsCurr<0">请选择规格</view>
			<image  v-if="mainData.type==1" src="../../static/images/details-icon2.png" class="jt-icon"></image>
		</view>
		
		<view class="flex p-3 line-h" v-if="mainData.type==2">
			<view class="color8 pr-5">规格</view>
			<view class="flex-1 pr-3" >x1</view>
		</view>
		
		<view class="f8-16"></view>
		
		<view  v-if="mainData.type==2">      <!-- 积分商品展示 -->
			<view class="color8 p-3">积分兑换说明</view>
			<view class="content" style="padding:0" v-html="tipData.content">
			</view>
		</view>
		<view class="f8-16"></view>
		
		<view>
			<view class="color8 p-3">详情</view>
			<view class="content" style="padding:0" v-html="mainData.content">
			</view>
		</view>
		
		
		<!-- 正常购买按钮 -->
		<view  v-if="mainData.type==1">
			<view style="height: 100rpx;"></view>
			<view class="p-fX bottom-0 bT-f5 flex1 bg-white">
				<view class="flex flex-1">
					<view class="flex4 font-22 bR-f5 w145 line-h" @click="Router.back({route:{delta:1}})">
						<image src="../../static/images/details-icon3.png" class="fh-icon mb-1"></image>
						<view>返回</view>
					</view>
					<view class="flex4 font-22 w145 line-h" @click="Router.redirectTo({route:{path:'/pages/car/car'}})">
						<image src="../../static/images/details-icon4.png" class="wh40 mb-1"></image>
						<view>购物车</view>
					</view>
				</view>
				<view class="btnBox flex">
					<view class="btn w-50 bg-3 colorf" @click="ggShow">加入购物车</view>
					<view class="btn w-50 btn1 Mgb" @click="ggShow">立即购买</view>
				</view>
			</view>
		</view>
		
		
		<!-- 积分商品兑换按钮 -->
		<view v-if="mainData.type==2">
			<view style="height: 170rpx;"></view>
			<view class="p-fX bottom-0 bT-f5">
				<view class="font-24 colorf jf text-center bg-7e" v-if="!canBuy">您的可用积分不足，去看看其他商品吧~</view>
				<view class="flex1 bg-white">
					<view class="flex">
						<view class="flex4 font-22 bR-f5 w145 line-h"
						@click="Router.back({route:{delta:1}})">
							<image src="../../static/images/details-icon3.png" class="fh-icon mb-1"></image>
							<view>返回</view>
						</view>
					</view>
					<view class="btnBox flex flex-1">
						<view class="btn w-100 btn1 Mgb" :class="!canBuy?'bg-f7':''" @click="goBuyScore">立即兑换</view>       <!-- 积分不足是增加gb-f7类名 -->
					</view>
				</view>
			</view>
		</view>
		
		
		
		<!-- 规格 -->
		<view class="bg-mask" v-show="gg_show">
			<view class="gg p-3 bg-white p-aX bottom-0">
				<view class="flex pb-2">
					<image :src="mainData.sku[specsCurr]&&mainData.sku[specsCurr].mainImg&&mainData.sku[specsCurr].mainImg[0]
					?mainData.sku[specsCurr].mainImg[0].url:''" class="wh200"></image>
					<view class="flex-1 pl-2">
						<view class="price1 font-40 pb-2">{{mainData.sku[specsCurr]?mainData.sku[specsCurr].price:''}}</view>
						<view class="font-24 color8">库存：{{mainData.sku[specsCurr]?mainData.sku[specsCurr].stock:'0'}}</view>
					</view>
					<view @click="ggShow">
						<image src="../../static/images/details-icon5.png" class="x-icon" style="width: 22rpx;height: 22rpx"></image>
					</view>
				</view>
				<view class="font-26 color2 py-3" v-for="(item,index) in labelData" :key="index">
					<view>{{item.title}}</view>
					<view class="flex flex-wrap signBox">
						<view class="tag" v-for="(c_item,c_index) in item.children"
						:class="Utils.inArray(c_item.id,choose_sku_item)==-1?'cantChoose'
						:(Utils.inArray(c_item.id,sku_item)!=-1?'on':'')"
						:key="c_index" :data-c_id="c_item.id" :data-id="item.id"
						@click="Utils.inArray($event.currentTarget.dataset.c_id,choose_sku_item)!=-1?
						chooseSku($event.currentTarget.dataset.id,$event.currentTarget.dataset.c_id):''"
						>
							{{c_item.title}}
						</view>
					</view>
				</view>
				<view class="flex1 pt-2">
					<view>数量</view>
					<view class="count">
						<view class="countIcon" @click="counter('-')"><image src="../../static/images/shopping-icon4.png" class="countIcon1"></image></view>
						<view class="countNum">{{count}}</view>
						<view class="countIcon" @click="counter('+')"><image src="../../static/images/shopping-icon3.png" class="countIcon2"></image></view>
					</view>
				</view>
				
				<view class="p-aX bottom-0 flex">
					<view class="btn w-50 bg3c colorf"  @click="addCar">加入购物车</view>
					<view class="btn w-50 Mgb" @click="goBuy">立即购买</view>
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
				gg_show:false,
				mainData: {},
				Utils:this.$Utils,
				labelData:[],
				skuData:[],
				specsCurr:0,
				sku_item:[],
				choose_sku_item:[],
				orderList:[],
				canBuy:true,
				showAll:false,
				count:1,
				tipData:{}
			}
		},
		onLoad(option) {
			const self = this;
			self.id = option.id;
			self.$Utils.loadAll(['getUserInfoData','getTipData'], self);
		},
		
		onShow() {
			const self = this;
			self.orderList = [];
			uni.removeStorageSync('payPro');
		},
		methods: {
			
			getTipData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					title:'积分兑换说明'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.tipData = res.info.data[0]
					}
					self.$Utils.finishFunc('getTipData');
				};
				self.$apis.articleGet(postData, callback);
			},
			
			ggShow(){
				const self = this;
				self.gg_show = !self.gg_show
			},
			
			goBuyScore(){
				const self = this;
				if(!self.canBuy){
					return
				};
				uni.setStorageSync('canClick',false);
				self.orderList.push(
					{product_id:self.mainData.id,count:1,
					type:self.mainData.type,product:self.mainData},
				);
				uni.setStorageSync('payPro', self.orderList);
				self.Router.navigateTo({route:{path:'/pages/submitOrder/submitOrder'}})
				uni.setStorageSync('canClick',true);
			},
			
			goBuy(){
				const self = this;
				if(!self.mainData.sku[self.specsCurr]){
					uni.setStorageSync('canClick',true);
					self.$Utils.showToast('请选择商品规格！', 'none');
					return
				};
				uni.setStorageSync('canClick',false);
				self.orderList.push(
					{sku_id:self.mainData.sku[self.specsCurr].id,count:self.count,
					type:self.mainData.type,product:self.mainData,skuIndex:self.specsCurr},
				);
				uni.setStorageSync('payPro', self.orderList);
				self.Router.navigateTo({route:{path:'/pages/submitOrder/submitOrder'}})
				uni.setStorageSync('canClick',true);
			},
			
			addCar() {
				const self = this;
				if(!self.mainData.sku[self.specsCurr]){
					uni.setStorageSync('canClick',true);
					self.$Utils.showToast('请选择商品规格！', 'none');
					return
				};
				var obj = self.mainData;
				self.mainData.skuIndex = self.specsCurr;
				self.mainData.skuId = self.mainData.sku[self.specsCurr].id;
				var array = self.$Utils.getStorageArray('cartData');
				for (var i = 0; i < array.length; i++) {
					if (array[i].skuId == self.mainData.sku[self.specsCurr].id) {
						var target = array[i]
					}
				};
				console.log(target)
				if (target) {
					target.count = target.count + 1
				} else {
					console.log(111)
					var target = self.mainData;
					target.count = self.count;
					target.isSelect = true;
				}
				self.$Utils.showToast('加入购物车成功', 'none');
				self.$Utils.setStorageArray('cartData', target, 'skuId', 999);
			},
			
			counter(type) {
				const self = this;
				if (type == '+') {
					self.count++;
				} else {
					if (self.count > 1) {
						self.count--;
					}
				};
				//self.countTotalPrice();
			},
			
			getUserInfoData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.noLoading = true;
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userInfoData = res.info.data[0];
						self.getMainData()
					};
				
				};
				self.$apis.userInfoGet(postData, callback);
			},
			
			getMainData() {
				var self = this;
				var postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					id: self.id
				};
				postData.getAfter = {
					sku: {
						tableName: 'Sku',
						middleKey: 'product_no',
						key: 'product_no',
						condition: '=',
						searchItem: {
							status: 1
						},
						order: {
							listorder: 'desc'
						}
					},
				};
				var callback = function(res) {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						
						if (self.mainData.type == 1) {
							for(var key in self.mainData.label){
							  if(self.mainData.sku_array.indexOf(parseInt(key))!=-1){
							    self.labelData.push(self.mainData.label[key])
							  };    
							};
							console.log('self.labelData',self.labelData)
							for (var i = 0; i < self.mainData.sku.length; i++) {
							  /* if(self.mainData.sku[i].id==self.id){
							    self.skuData = self.$Utils.cloneForm(self.mainData.sku[i]);
							  }; */
											
							  self.choose_sku_item.push.apply(self.choose_sku_item,self.mainData.sku[i].sku_item);
							};
							if(self.mainData.sku[0]){
								self.skuData = self.$Utils.cloneForm(self.mainData.sku[0]);
								self.sku_item = self.skuData.sku_item;
							}
							
						}else{
							if(parseFloat(self.userInfoData.score)<parseFloat(self.mainData.price)){
								self.canBuy = false
							}
						};
						self.showAll = true
					};
					self.$Utils.finishFunc('getUserInfoData');
				};
				self.$apis.productGet(postData, callback);
			},
			
			chooseSku(parentid,id){
				const self = this;
			    self.skuData = {};
			    if(self.choose_sku_item.indexOf(id)==-1){
			      return;
			    };
				self.specsCurr = -1;
			    self.choose_sku_item = [];
			    var sku = self.mainData.label[parentid];
			    for(var i=0;i<sku.children.length;i++){
			      if(self.sku_item.indexOf(sku.children[i].id)!=-1){
			        self.sku_item.splice(self.sku_item.indexOf(sku.children[i].id), 1);
			      };
			      self.choose_sku_item.push(sku.children[i].id);
			    };
			
			    
			    for (var i = 0; i < self.mainData.sku.length; i++) {
			      if(self.mainData.sku[i].sku_item.indexOf(parseInt(id))!=-1){
			        self.choose_sku_item.push.apply(self.choose_sku_item,self.mainData.sku[i].sku_item);  
			      };
			    };
			
			    for(var i=0;i<self.sku_item.length;i++){
			      if(self.choose_sku_item.indexOf(parseInt(self.sku_item[i]))==-1){
			        self.sku_item.splice(i, 1); 
			      };
			    };
			    self.sku_item.push(id);
			    for(var i=0;i<self.mainData.sku.length;i++){ 
			      if(JSON.stringify(self.mainData.sku[i].sku_item.sort())==JSON.stringify(self.sku_item.sort())){
			        //self.id = self.mainData.sku[i].id;
			        self.skuData = self.$Utils.cloneForm(self.mainData.sku[i]);
					self.specsCurr = i
			      };   
			    }; 
			},
		}
	}
</script>

<style scoped>
.swiper-box,.swiper-item,.swiper-item image{width: 750rpx;height: 750rpx;}
.btnBox{width: 460rpx;}
.w145{width: 145rpx;}

.gg{height: 800rpx;}
.gg .wh200{margin-top: -100rpx;}
.gg .tag{width: 200rpx;line-height: 64rpx;text-align: center;border-radius: 10rpx;border: 1px solid #e5e5e5;margin: 30rpx 30rpx 0 0;}
.gg .on{background-color: #E6B968;border: none;}
.gg .signBox{max-height: 330rpx;overflow-y: auto;}
.bg-d7{background-color: #d7d7d7;}
.bg-7e{background-color: #7F7F7F;}
.jf{line-height: 70rpx;}
</style>
