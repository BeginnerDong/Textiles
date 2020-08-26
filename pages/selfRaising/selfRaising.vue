<template>
	<view>
		
		<view>
			<view class="flex1 px-3 py-4 p-r line-h"
			@click="Router.navigateTo({route:{path:'/pages/selfRaising/selfRaising'}})">
				<view class="addressTxt">
					<view class="font-30 font-w avoidOverflow">陕西省西安市雁塔区科技路高新大都荟A座2007</view>
					<view class="font-26 color6 pt-3">商家名称 <text class="pl-4">18228926587</text></view>
				</view>
				<image src="../../static/images/shopping-icon.png" class="wh36"></image>
				<!-- <image src="../../static/images/shopping-icon1.png" class="wh36"></image> -->
			</view>
			<view class="f720"></view>
		</view>
		
		
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
.addressTxt{width: 630rpx;}
</style>
