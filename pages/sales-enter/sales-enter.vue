<template>
	<view>
		
		<view class="info p-3 colorf">
			<view class="text-right font-26">退出</view>
			<view class="flex4">
				<image src="../../static/images/thesalesman-icon4.png" class="wh130"></image>
				<view class="font-30 pt-3 pb-2 line-h font-w">清风微笑</view>
				<view class="font-20 color6 bg-f5 radius10 p-1 line-h ">店铺名称</view>
			</view>
			<view class="flex1 font-22 line-h pt-4 pb-2">
				<view class="flex4 w-50"
				@click="Router.navigateTo({route:{path:'/pages/sales-qrcode/sales-qrcode'}})">
					<image src="../../static/images/thesalesman-icon.png" class="wh40 mb-2"></image>
					<view>推广二维码</view>
				</view>
				<view class="flex4 w-50"
				@click="Router.navigateTo({route:{path:'/pages/sales-user/sales-user'}})">
					<view class="wh40 mb-2 font-48 font-w">28</view>
					<view>推广用户</view>
				</view>
			</view>
		</view>
		
		<view class="list mb-2">
			<view class="li" :class="liCurr==0?'on':''" @click="changeLi(0)">全部</view>
			<view class="li" :class="liCurr==1?'on':''" @click="changeLi(1)">待核销</view>
			<view class="li" :class="liCurr==2?'on':''" @click="changeLi(2)">已核销</view>
		</view>
		
		<view class="font-24 bg-white p-3"
		@click="Router.navigateTo({route:{path:'/pages/orderDetail/orderDetail'}})">
			<view class="flex1">
				<!-- <image src="../../static/images/theorder-icon.png" class="wh28"></image> -->
				<image src="../../static/images/theorder-icon1.png" class="wh28"></image>
				<view class="flex-1 pl-1">2020.07.30 11:00:34</view>
				<view class="colorR">已核销</view>
			</view>
			<view class="pt-3 flex1">
				<view class="flex">
					<image src="../../static/images/thesalesman-img.png" class="wh160"></image>
					<image src="../../static/images/thesalesman-img.png" class="wh160"></image>
					<image src="../../static/images/thesalesman-img.png" class="wh160"></image>
				</view>
				<view class="line-h text-right">
					<view class="font-32 font-w price1">6980.00</view>
					<view class="color8 pt-2">共3件</view>
				</view>
			</view>
		</view>
		
		<image src="../../static/images/thesalesman-icon1.png" class="wh100 p-f right-0"
		@click="Router.navigateTo({route:{path:'/pages/sales-hxOrder/sales-hxOrder'}})"></image>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				liCurr:0
			}
		},
		methods: {
			
			changeLi(i){
				const self = this;
				self.liCurr = i
			}
			
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
