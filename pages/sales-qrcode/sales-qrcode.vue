<template>
	<view>
		
		<image src="../../static/images/thesalesman-icon6.png" class="p-fXY" ></image>
		
		<view class="p-r">
			<view class="tg">推广二维码</view>
			<image :src="qrUrl" class="wh400"></image>
		</view>
		<view class="bg-white px-3 py-2 bT-e1 p-fX bottom-0" @click="savePoster">
			<view class="btn80 Mgb">保存到相册</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				qrUrl:''
			}
		},
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getQrCode'], self);
		},
		methods: {
			
			savePoster() {
				let self = this
				//若二维码未加载完毕，加个动画提高用户体验
				wx.showToast({
					icon: 'loading',
					title: '正在下载图片',
					duration: 1000
				})
				//判断用户是否授权"保存到相册"
				wx.getSetting({
					success(res) {
						//没有权限，发起授权
						if (!res.authSetting['scope.writePhotosAlbum']) {
							wx.authorize({
								scope: 'scope.writePhotosAlbum',
								success() { //用户允许授权，保存图片到相册
									self.savePhoto();
								},
								fail() { //用户点击拒绝授权，跳转到设置页，引导用户授权
									console.log('fail')
									wx.showToast({
										icon: 'none',
										title: '请至小程序设置中开启相册权限',
										duration: 1000
									})
								}
							})
						} else { //用户已授权，保存到相册
							self.savePhoto()
						}
					}
				})
			},
			
			savePhoto() {
				let self = this
				wx.saveImageToPhotosAlbum({
					filePath: self.qrUrl,
					success(res) {
						wx.showToast({
							title: '保存成功',
							icon: "success",
							duration: 1000
						})
					}
				})
			},
			
			getQrCode() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getSalesToken'
				postData.qrInfo = {
					scene:uni.getStorageSync('sales_info').info.phone,
					page: 'pages/index/index',
				};
				postData.output = 'url';
				postData.ext = 'png';
				const callback = (res) => {
					if (res.solely_code == 100000) {
						self.qrUrl = res.info.url
					}
					self.$Utils.finishFunc('getQrCode');
				};
				self.$apis.getQrCode(postData, callback);
			},
			
		}
	}
</script>

<style>
page{background-color: #E6B968}
.tg{font-size: 60rpx;font-weight: bold;text-align: center;margin-top: 30%;}
.wh400{width: 400rpx;height: 400rpx;margin: 50rpx auto;}
</style>
