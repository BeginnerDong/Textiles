<template>
	<view class="px-3">
		
		<view class="py-4 bB-f5 flex1 line-h">
			<view>姓名</view>
			<input type="text" v-model="submitData.name" placeholder="填写姓名" placeholder-style="color:#999;" />
		</view>
		<view class="py-4 bB-f5 flex1 line-h">
			<view>手机号</view>
			<input type="text" v-model="submitData.phone" placeholder="填写手机号" placeholder-style="color:#999;"  />
		</view>
		<view class="py-4 bB-f5 flex1 line-h">
			<view>生日</view>
			<picker mode="date" class="flex-1 text-right" @change="brithdayChnage">
				<view class="" :class="submitData.birthday!=''?'color2':'color9'">{{submitData.birthday!=''?submitData.birthday:'请选择'}}</view>
			</picker>
			<image src="../../static/images/details-icon2.png" class="jt-icon ml-1"></image>
		</view>
		<view class="py-4 bB-f5 flex1 line-h">
			<view>所在地区</view>
			<picker mode="region" class="flex-1 text-right" @change="regionChange">
				<view class="" :class="submitData.region!=''?'color2':'color9'">{{submitData.region!=''?submitData.region:'请选择'}}</view>
			</picker>
			<image src="../../static/images/details-icon2.png" class="jt-icon ml-1"></image>
		</view>
		<view class="py-4 bB-f5 flex1 line-h">
			<view>详细地址</view>
			<input type="text" v-model="submitData.address" placeholder="请填写" placeholder-style="color:#999;"  />
		</view>
		
		<view class="btn80 Mgb mt-4"  @click="Utils.stopMultiClick(submit)">立即注册</view>
		
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Utils:this.$Utils,
				submitData:{
					name:'',
					phone:'',
					region:'',
					address:'',
					birthday:'',
					
				}
			}
		},
		onLoad(options) {
			const self = this;
			self.$Utils.loadAll(['getUserInfoData'], self);
		},
		methods: {
			
			brithdayChnage(e){
				const self = this;
				self.submitData.birthday = e.detail.value
			},
			
			regionChange(e){
				const self = this;
				self.submitData.region = e.detail.value[0]+e.detail.value[1]+e.detail.value[2]
			},
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				if(self.submitData.name == ''){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请填写姓名', 'none')
					return
				};
				if(self.submitData.phone == ''){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请填写电话号', 'none')
					return
				};
				if(self.submitData.brithday == ''){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请选择生日', 'none')
					return
				};
				if(self.submitData.address == ''){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请填写地址', 'none')
					return
				};
				if(self.submitData.region == ''){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请选择地区', 'none')
					return
				};
				self.userInfoUpdate();
				/* const pass = self.$Utils.checkComplete(self.submitData);
				console.log('pass', pass);
				console.log('self.submitData',self.submitData)
				
				if (pass) {	
					self.userInfoUpdate();
				} else {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请补全信息', 'none')
				}; */
			},
			
			userInfoUpdate(){
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				var newObject = self.$Utils.cloneForm(self.submitData);
				postData.data = self.$Utils.cloneForm(newObject);
				postData.searchItem = {
					user_no:uni.getStorageSync('user_info').user_no
				};
				const callback = (res) => {
					if (res.solely_code==100000) {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('完善成功', 'none');
						setTimeout(function() {
							uni.navigateBack({
								delta:1
							})
						}, 1000);
					}else{
						self.$Utils.showToast(res.msg, 'none');
					}
				};
				self.$apis.userInfoUpdate(postData, callback);
			},
			
			getUserInfoData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userInfoData = res.info.data[0];
						self.submitData.name = self.userInfoData.name
						self.submitData.phone = self.userInfoData.phone
						self.submitData.region = self.userInfoData.region
						self.submitData.address = self.userInfoData.address
						self.submitData.birthday = self.userInfoData.birthday
					}
					self.$Utils.finishFunc('getUserInfoData');
				};
				self.$apis.userInfoGet(postData, callback);
			},
			
		}
	}
</script>

<style scoped>
input{flex: 1;text-align: right;line-height: 1;}
</style>
