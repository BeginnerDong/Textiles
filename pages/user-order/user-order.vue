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
			<view class="li li1" :class="liCurr==0?'on':''" @click="changeLi(0)">全部</view>
			<view class="li li1" :class="liCurr==1?'on':''" @click="changeLi(1)">待支付</view>
			<view class="li li1" :class="liCurr==2?'on':''" @click="changeLi(2)">待核销</view>
			<view class="li li1" :class="liCurr==3?'on':''" @click="changeLi(3)">已核销</view>
		</view>
		
		
		
		<view class="font-24 bg-white p-3"
		@click="Router.navigateTo({route:{path:'/pages/orderDetail/orderDetail'}})">
			<view class="flex1">
				<!-- <image src="../../static/images/theorder-icon.png" class="wh28"></image> -->
				<image src="../../static/images/theorder-icon1.png" class="wh28"></image>
				<view class="flex-1 pl-1">2020.07.30 11:00:34</view>
				<view class="colorR">已完成</view>
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
			<view class="d-flex j-end pt-3">
				<view class="btnOrder">取消订单</view>
				<view class="btnOrder order2">去支付</view>
				<view class="btnOrder order2">确认收货</view>
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
				type:0
			}
		},
		onLoad(options){
			const self = this;
			self.type = options.type
		},
		methods: {
			
			changeLi(i){
				const self = this;
				self.liCurr = i
			}
			
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
