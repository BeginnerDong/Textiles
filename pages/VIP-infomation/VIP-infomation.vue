<template>
	<view class="px-3">
		
		<view class="py-4 bB-f5 flex1 line-h">
			<view>姓名</view>
			<input type="text" value="" placeholder="填写姓名" placeholder-style="color:#999;" />
		</view>
		<view class="py-4 bB-f5 flex1 line-h">
			<view>手机号</view>
			<input type="text" value="" placeholder="填写手机号" placeholder-style="color:#999;"  />
		</view>
		<view class="py-4 bB-f5 flex1 line-h">
			<view>生日</view>
			<picker mode="date" class="flex-1 text-right">
				<view class="color9 font-22">请选择</view>
			</picker>
			<image src="../../static/images/details-icon2.png" class="jt-icon ml-1"></image>
		</view>
		<view class="py-4 bB-f5 flex1 line-h">
			<view>所在地区</view>
			<picker mode="region" class="flex-1 text-right">
				<view class="color9 font-22">请选择</view>
			</picker>
			<image src="../../static/images/details-icon2.png" class="jt-icon ml-1"></image>
		</view>
		<view class="py-4 bB-f5 flex1 line-h">
			<view>详细地址</view>
			<input type="text" value="" placeholder="请填写" placeholder-style="color:#999;"  />
		</view>
		
		<view class="btn80 Mgb mt-4">立即注册</view>
		
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped>
input{flex: 1;text-align: right;line-height: 1;font-size: 22rpx;}
</style>
