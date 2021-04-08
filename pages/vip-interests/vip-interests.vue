<template>
	<view>
		<view>
			<view class="p-aX">
				<image src="../../static/images/quanyi-img4.jpg" mode="widthFix"></image>
			</view>
			<view class="pt-2 flex2 z1 p-r">
				<image src="../../static/images/quanyi-img2.jpg" mode="widthFix" style="width: 670rpx;"></image>
				<view class="p-aXY" style="padding-top: 100rpx">
					<view class="text-center font-60 font-w" style="color: #3d2d1c;">家纺尊享会员</view>
				</view>
			</view>
			<view class="flex2 z1 p-r"  style="margin-top: -100rpx;">
				<image src="../../static/images/quanyi-img.png" mode="widthFix"></image>
				<view class="p-aXY" style="padding-top: 130rpx">
					<view class="d-flex j-center a-center">
						<image src="../../static/images/quanyi-icon4.png" mode="widthFix" class="icon"></image>
						<view class="px-2 font-36 font-w" style="color: #3d2d1c;">会员权益</view>
						<image src="../../static/images/quanyi-icon4.png" mode="widthFix" class="icon"></image>
					</view>
					<view class="px-5 flexX pt-5">
						<view class="item flex-shrink" v-for="(item,index) in labelData"  :key="index"
						@click="Router.navigateTo({route:{path:'/pages/interestsDetail/interestsDetail?index='+index}})">
							<view class="d-flex j-center">
								<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''"></image>
							</view>
							
							<view class="font-26 color2 pt-2">{{item.title}}</view>
						</view>
					</view>
				</view>
			</view>
			<view style="margin-top: -15rpx;">
				<view class="content" style="padding:0" v-html="mainData.content">
				</view>
			</view>
		</view>
		<view style="height: 120rpx;"></view>
		<view class="bottom d-flex a-center" @click="Router.navigateTo({route:{path:'/pages/VIP-infomation/VIP-infomation'}})">
			<view class="join">立即领取</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mainData:{},
				Router:this.$Router,
				labelData:[]
			}
		},
		onLoad() {
			const self = this;
			 self.$Utils.loadAll(['getMainData','getLabelData'], self);
		},
		methods: {
			
			getLabelData() {
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
						self.labelData = res.info.data
					}
					self.$Utils.finishFunc('getLabelData');
				};
				self.$apis.articleGet(postData, callback);
			},
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					title:'会员权益'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0]
						const regex = new RegExp('<img', 'gi');
						self.mainData.content = self.mainData.content.replace(regex, `<img style="max-width: 100%;height:auto"`);
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
		}
	}
</script>

<style>
	.icon{width: 50rpx;height: 34rpx;}
	.item image{width: 90rpx;height: 90rpx;}
	.item{margin-right: 78rpx;text-align: center;}
	
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
