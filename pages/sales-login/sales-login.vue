<template>
	<view class="sales line-h">
		<image src="../../static/images/thelogin-img.png" class="p-fX bottom-0" mode="widthFix"></image>
		
		<view class="p-r">
			<view class="font-52 font-w">登录</view>
			
			<view class="font-32 font-w tit">账号</view>
			<input type="text" v-model="submitData.login_name" placeholder="请输入" />
			<view class="font-32 font-w tit">密码</view>
			<input type="text" v-model="submitData.password" placeholder="请输入" />
			
			<view class="btn80 Mgb shadow z10"
			@click="submit">登录</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
				submitData:{
					login_name:'',
					password:''
				},
				Router:this.$Router
			}
		},
		methods: {
			
			submit() {
				const self = this;
				const postData = {
					login_name: self.submitData.login_name,
					password:self.submitData.password
				};
				if (self.$Utils.checkComplete(self.submitData)) {
					const callback = (res) => {
						if (res.solely_code == 100000) {
							self.$Utils.showToast('登陆成功','none')
							uni.setStorageSync('sales_token', res.token);
							uni.setStorageSync('sales_info', res.info);
							setTimeout(function() {
								self.Router.redirectTo({route:{path:'/pages/sales-enter/sales-enter'}})
							}, 1000);
						} else {
							self.$Utils.showToast(res.msg,'none')
						}
					}
					self.$apis.saleLogin(postData, callback);
				} else {
					self.$Utils.showToast('请补全登录信息', 'none')
				};
			},
			
		}
	}
</script>

<style scoped>
.sales{padding: 16% 70rpx 0;}
input{padding: 30rpx 0;font-size: 26rpx;line-height: 1;border-bottom: 1px solid #f5f5f5;}
.tit{padding: 80rpx 0 10rpx;}
.btn80{margin-top: 160rpx;}
</style>
