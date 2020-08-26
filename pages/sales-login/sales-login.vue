<template>
	<view class="sales line-h">
		<image src="../../static/images/thelogin-img.png" class="p-fX bottom-0" mode="widthFix"></image>
		
		<view class="p-r">
			<view class="font-52 font-w">登录</view>
			
			<view class="font-32 font-w tit">账号</view>
			<input type="text" value="" placeholder="请输入" />
			<view class="font-32 font-w tit">密码</view>
			<input type="text" value="" placeholder="请输入" />
			
			<view class="btn80 Mgb shadow z10"
			@click="Router.navigateTo({route:{path:'/pages/sales-enter/sales-enter'}})">登录</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped>
.sales{padding: 16% 70rpx 0;}
input{padding: 30rpx 0;font-size: 26rpx;line-height: 1;border-bottom: 1px solid #f5f5f5;}
.tit{padding: 80rpx 0 10rpx;}
.btn80{margin-top: 160rpx;}
</style>
