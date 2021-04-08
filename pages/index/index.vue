<template>
	<view class="p-r">
		<image src="../../static/images/img.png"  class="p-aXY bgImg"></image>
		<view class="py-2">
			<view class="flex font-24 color8 px-3 mx-3  p-r  ss"
			@click="Router.navigateTo({route:{path:'/pages/search/search'}})">
				<image src="../../static/images/home-icon.png" class="wh36 mr-3"></image>
				<view>搜索想要找的商品</view>
			</view>	
		</view>
		
		<!-- banner/搜索框 -->
		<view class="p-r">
			<swiper class="swiper-box" indicator-dots="indicatorDots" autoplay="autoplay" interval="3000" indicator-active-color="#E6B968">
				<block>
					<swiper-item class="swiper-item" v-for="(item,index) in sliderData" :key="index">
						<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode="widthFix" />
					</swiper-item>
				</block>
			</swiper>
			
			
		</view>
		
		<!-- 金刚区 -->
		<view class="font-26 color2 line-h mt-4 p-r flex2">
			<view class="flex4"
			@click="Router.navigateTo({route:{path:'/pages/vip-interests/vip-interests'}})">
				<image src="../../static/images/home-icon0.png" class="icon mb-2"></image>
				<view>会员权益</view>
			</view>
			<view class="flex4" 
			@click="Router.navigateTo({route:{path:'/pages/integralShop/integralShop'}})">
				<image src="../../static/images/home-icon1.png" class="icon mb-2"></image>
				<view>积分商城</view>
			</view>
			<view class="flex4"
			@click="Router.navigateTo({route:{path:'/pages/store/store'}})">
				<image src="../../static/images/home-icon2.png" class="icon mb-2"></image>
				<view>门店信息</view>
			</view>
			<button open-type="contact" style="border-radius: 0;" class="line-h font-26 flex4">
				<image src="../../static/images/home-icon3.png" class="icon mb-2"></image>
				<view>联系我们</view>
			</button>
		</view>
		
		<!-- 优惠券 -->
		<view class="mx-3 mt-5 pb-3 p-r" @click="Router.navigateTo({route:{path:'/pages/user-coupon/user-coupon'}})">
			<image src="../../static/images/home-img.jpg" mode="widthFix"></image>
		</view>
		
		<!-- 品牌 -->
		<view class="p-r font-34 font-w flex0 mt-4">
			<view class="p-r pp">
				精选品牌
				<image src="../../static/images/home-icon4.png" class="wh40 p-a"></image>
			</view>
		</view>
		<view class="p-r px-3 flex mt-2">
			<view class="flex4 mr-r" v-for="(item,index) in brandData" :key="index"
			:data-id="item.id" @click="Router.redirectTo({route:{path:'/pages/classify/classify?brandId='+$event.currentTarget.dataset.id}})"
			>
				<view class="flex0 pp-b radius10 px-3">
					<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode="widthFix" class="ppIcon"></image>
				</view>
				<view class="flex0 font-18 color2 pt-2 Mgb radius10 pp-y">
					<view>查看商品</view>
					<image src="../../static/images/home-icon5.png" class="jt-icon1 ml-1"></image>
				</view>
			</view>
		</view>
		
		<!-- 套件系列 -->
		<view class="p-r m-2 mt-3 py-3" v-if="item.product&&item.product.length>0" v-for="(item,index) in mainData" :key="index">
			<image src="../../static/images/home-img3.png" mode="widthFix" class="p-aX"></image>
			<view class="font-34 font-w text-center mt-5 pt-2">{{item.title}}</view>
			<view class="mt-5 d-flex py-2 px-4 j-sb a-start">
				<view class="w300" v-for="(c_item,c_index) in item.product" 
				:data-id="c_item.id" :key="c_index"
				@click="Router.navigateTo({route:{path:'/pages/goodDetail/goodDetail?id='+$event.currentTarget.dataset.id}})">
					<image :src="c_item.mainImg&&c_item.mainImg[0]?c_item.mainImg[0].url:''" class="wh300"></image>
					<view class="avoidOverflow2 pt-1" style="height: 86rpx;">{{c_item.title}}</view>
					<view class="price1 font-32 font-w pt-2">{{c_item.price}}</view>
					<view  class="font-24 color6" style="text-decoration: line-through;">市场价：{{c_item.o_price?c_item.o_price:'0.00'}}</view>
				</view>
			</view>
			<view class="moreBtn font-26 flex0 z100"
			 @click="Router.redirectTo({route:{path:'/pages/classify/classify?'}})">
				<view class="z100" style="width: 55%;height: 100%;">查看更多</view>
				<image src="../../static/images/home-icon6.png" class="jt-icon2"></image>
			</view>
		</view>
		
		<view class="bg-mask z1000 line-h" v-show="is_show1">
			<view class="p-aX bottom-0 radius20-T bg-white font-30 pt-3 flex5">
				<view class="text-center" style="font-weight: 700;font-size:18px">提示</view>
				<view class="text-center" style="padding:50rpx 0;">请同意授权使用小程序</view>
				<button class="flex0 bg-white py-2 bT-f5" open-type="getUserInfo" @getuserinfo="Utils.stopMultiClick(submit)">
					<view class="grayBtn linearBtn">确定</view>
				</button>
			</view>
		</view>
		
		
		<view style="height: 130rpx;"></view>
		<!-- footer -->
		<view class="footer">
			<view class="item on" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1-a.png" mode=""></image>
				<view>首页</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/classify/classify'}})">
				<image src="../../static/images/nabar2.png" mode=""></image>
				<view>分类</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/car/car'}})">
				<image src="../../static/images/nabar3.png" mode=""></image>
				<view>购物车</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})">
				<image src="../../static/images/nabar4.png" mode=""></image>
				<view>我的</view>
			</view>
		</view>
		
		<button open-type="contact" style="position: fixed;bottom: 40%;right: 2%;z-index: 10">
			<image src="../../static/images/kefu.png" style="width: 70rpx;height: 70rpx;">
			<view class="colorM font-28">客服</view>
		</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				is_show: false,
				sliderData:[],
				brandData:[],
				mainData:[],
				is_show1:false,
				Utils:this.$Utils,
			}
		},
		onLoad(options) {
			const self = this;
			if(options.scene){
				var scene  = decodeURIComponent(options.scene)
				const callback = (res) => {
					self.$Utils.loadAll(['getSliderData','getBrandData','getMainData'], self);
				};
				self.$Token.getProjectToken(callback, {
					refreshToken: true,
					parent_no: scene
				})
			}else{
				self.$Utils.loadAll(['getSliderData','getBrandData','getMainData'], self);
			}
		},
		onShow() {
			const self = this;
			self.getUserData()
		},
		methods: {
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);	
				const callback = (user, res) => {
					console.log(res)
					self.getUserData(user);
				};
				self.$Utils.getAuthSetting(callback);
			},
			
			getUserData(user) {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				if(!user){
					postData.noLoading = true;
				};
				if(user){
					postData.refreshToken = true;
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0];
						if(self.userData.headImgUrl == ''){
							self.is_show1 = true
						}else{
							self.is_show1 = false
						}
					};
				};
				self.$apis.userGet(postData, callback);
			},
			
			getMainData() {
				const self = this;
				const postData = {};
				/* postData.paginate =  {
					count: 0,
					currentPage:1,
					pagesize:3,
					is_page:true,
				}, */
				postData.searchItem = {
					thirdapp_id: 2,
					type: 3,
					id:['not in',[4]]
				};
				postData.getAfter = {
					product:{
						tableName:'Product',
						middleKey:'id',
						key:'category_id',
						searchItem:{
							status:1
						},
						condition:'=',
						paginate:{
							currentPage:1,
							pagesize:2,
						},
					},
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			getBrandData() {
				const self = this;
				const postData = {};
				postData.paginate =  {
					count: 0,
					currentPage:1,
					pagesize:3,
					is_page:true,
				},
				postData.searchItem = {
					thirdapp_id: 2,
					type: 2
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.brandData = res.info.data
					}
					self.$Utils.finishFunc('getBrandData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			getSliderData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					menu_id: 1
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.sliderData = res.info.data
					}
					self.$Utils.finishFunc('getSliderData');
				};
				self.$apis.articleGet(postData, callback);
			},
		}
	};
</script>

<style scoped>
.swiper-box,.swiper-item{height: 410rpx;}
.ss{height: 60rpx;line-height: 60rpx;border-radius: 30rpx;background-color: rgba(255,255,255);top: 0;}
.icon{width: 51rpx;height: 54rpx;}
.bgImg{}

.pp image{top: -22rpx;right: -32rpx;}
.pp-b{width: 210rpx;height: 100rpx;background-color: #2A2A2A;z-index: 5;}
/* .ppIcon{height: 20rpx;} */
.pp-y{width: 180rpx;height: 58rpx;margin-top: -20rpx;}
.mr-r{margin-right: 30rpx;}
.mr-r:nth-child(3n){margin-right: 0rpx;}
.grayBtn{background-color: #E6B968;color: #666;line-height: 80rpx;border-radius: 40rpx;text-align: center;font-size: 30rpx;width: 260rpx;}
</style>