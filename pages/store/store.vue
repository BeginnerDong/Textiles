<template>
	<view>
		
		<view class="pl-3 flex1" v-for="v in 3" :key="v">
			<image src="../../static/images/stores-img.png" class="wh180"></image>
			<view class="color2 font-26 pl-2 pr-3 py-4 bB-f5 h240 flex-1 flex5">
				<view class="font-32 font-w flex-1">三五八CLUB</view>
				<view class="flex pb-2"> 
					<image src="../../static/images/stores-icon.png" class="wh26 mr-1"></image>
					<view>13562847950</view>
				</view>
				<view class="flex1">
					<image src="../../static/images/stores-icon1.png" class="dw-icon mr-1"></image>
					<view class="flex-1">雁塔区高新大都荟A座2007</view>
					<view class="font-24 color8">2.4km</view>
				</view>
			</view>
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
.h240{height: 240rpx;}
</style>
