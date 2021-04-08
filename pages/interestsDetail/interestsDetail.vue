<template>
	<view>
		<button open-type="contact" style="position: fixed;bottom: 35%;right: 2%;z-index: 10">
			<image src="../../static/images/kefu.png" style="width: 70rpx;height: 70rpx;">
			<view class="colorM font-28">客服</view>
		</button>
		<view class="p-aX">
			<image src="../../static/images/quanyi-img3.jpg" mode="widthFix"></image>
		</view>
		<view class="p-r">
			<swiper  style="height: 240rpx;" class="swiper-box"  :autoplay="autoplay" :current="index" @change="change">
				<block>
					<swiper-item class="swiper-item">
						
					</swiper-item>
					<swiper-item class="swiper-item" v-for="(item,i) in mainData"  :key="i">
						<view class="item flex4" :style="index!=i?'opacity:0.3':''" >
							
							<image  :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''"></image>
							<view   class="font-26 color2 pt-2">{{item.title?item.title:''}}</view>
						</view>
					</swiper-item>
				</block>
			</swiper>
			<view class="px-3 mb-2 bg-white">
				<view class="bB-e1">
					<view class="font-30 color2 py-3">权益对象</view>
				</view>
				<view class="font-26 color6 py-3">
					<view class="content" style="padding:0" v-html="mainData[index].content">
					</view>
				</view>	
			</view>
			
			<view class="px-3  bg-white">
				<view class="bB-e1">
					<view class="font-30 color2 py-3">权益说明</view>
				</view>
				<view class="font-26 color6 py-3">
					<view class="content" style="padding:0" v-html="mainData[index].passage1">
					</view>
				</view>	
			</view>
		</view>
	</view>
</template>

<script>
	import container from '../../components/container/index.vue'
	import LsSwiper from '../../components/ls-swiper/index.vue'
	export default {
		data() {
			return {
				mainData:{},
				autoplay:false,
				sliderData:[{url:'../../static/images/quanyi-icon.png',title:"上门试铺"},{url:'../../static/images/quanyi-icon1.png',title:"上门试铺"},
				{url:'../../static/images/quanyi-icon2.png',title:"上门试铺"},{url:'../../static/images/quanyi-icon3.png',title:"上门试铺"},],
				index:0
			}
		},
		components:{
			container,
			LsSwiper
		},
		onLoad(options) {
			const self = this;
			self.index = options.index;
			 self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			change(e){
				const self = this;
				console.log(e)
				self.index = e.detail.current;
				if(e.detail.current==self.mainData.length){
					self.index = 0
				}
				console.log(self.index)
			},
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					title:['not in',['会员权益','积分兑换说明']],
					menu_id:3
				};
				postData.order = {
					listorder:'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data;
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
		}
	}
</script>

<style>
	page{background-color: #F5F5F5;}
	.swiper-item{width: 33.3%!important;overflow: initial;}
	.icon{width: 50rpx;height: 34rpx;}
	.item image{width: 90rpx;height: 90rpx;}
	.item{height: 100%;}
	.bottom{width: 750rpx;
	height: 120rpx;
	background-color: #ffffff;
	box-shadow: 0px 0px 12rpx 0px 
		rgba(0, 0, 0, 0.08);
		position: fixed;
		bottom: 0;
		}
		.join{width: 690rpx;
	height: 80rpx;
	background-color: #e6b968;margin: 0 auto;color: #222222;font-size: 32rpx;text-align: center;line-height: 80rpx;}
</style>
