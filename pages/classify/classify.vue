<template>
	<view>
		
		<view class="p-s top-0 bg-white z10 pt-3">
			<view class="flex font-24 color8 px-3 mx-3 b-e1 flex-1 ss">
				<image src="../../static/images/home-icon.png" class="wh36 mr-3"></image>
				<input type="text" value="" placeholder="搜索想要找的商品" />
			</view>
			<view class="font-30 color8 line-h bB-e1 flex1 mb-3 sx">
				<view class="item" @click="change(0)" :class="sxCurr==0?'colorM':''">综合</view>
				<view class="item" @click="change(1)" :class="sxCurr==1?'colorM':''">销量</view>
				<view class="flex item" @click="change(2)" :class="sxCurr==2?'colorM':''">
					<view>价格</view>
					<view class="pl-1">
						<image src="../../static/images/classification-icon1.png" class="sxIcon mb-1"></image>
						<image src="../../static/images/classification-icon2.png" class="sxIcon"></image>
					</view>
				</view>
				<view class="flex item" @click="change(3)" :class="sxCurr==3?'colorM':''">
					<view>筛选</view>
					<image src="../../static/images/classification-icon.png" class="sxIcon1 ml-1"></image>
				</view>
			</view>
		</view>
		
		<!-- 搜索结果 -->
		<view class="flex1 px-3 pb-4" v-for="v in 10"
		@click="Router.navigateTo({route:{path:'/pages/goodDetail/goodDetail'}})">
			<image src="../../static/images/classification-img.png" class="listImg"></image>
			<view class="flex5 font-30 py-0 flex-1 pl-2 h213">
				<view class="avoidOverflow2">ROYALCOVER_罗卡芙家纺 浪漫婚典 真丝绣花提花九件套 爱的乐章</view>
				<view class="flex1">
					<view class="price1 font-32 font-w">6980.00</view>
					<image src="../../static/images/classification-icon3.png" class="wh52"></image>
				</view>
			</view>
		</view>
		
		<!-- 筛选弹框 -->
		<view class="bg-mask" v-show="sx_show">
			<view class="w600 bg-white p-aY right-0 font-24 line-h flex5 sx">
				<view class="sxbg p-2 pt-3">筛选</view>
				<view class="flex-1 flexY sxCon">
					<view class="p-2 mt-1 bB-f5" v-for="v in 2" :key="v">
						<view>品牌</view>
						<view class="flex flex-wrap">
							<view class="sign on">罗卡芙</view>
							<view class="sign">罗卡芙</view>
							<view class="sign">罗卡芙</view>
							<view class="sign">罗卡芙</view>
							<view class="sign">罗卡芙</view>
						</view>
					</view>
				</view>
				
				<view class="p-aX bottom-0 flex colorf">
					<view class="btn w-50 bg3c">重置</view>
					<view class="btn w-50 Mgb" @click="close">确定</view>
				</view>
			</view>
		</view>
		
		
		<view style="height: 130rpx;"></view>
		<!-- footer -->
		<view class="footer">
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1.png" mode=""></image>
				<view>首页</view>
			</view>
			<view class="item on">
				<image src="../../static/images/nabar2-a.png" mode=""></image>
				<view>分类</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/car/car'}})">
				<image src="../../static/images/nabar3.png" mode=""></image>
				<view>购物车</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})">
				<image src="../../static/images/nabar4.png" mode=""></image>
				<view>我的</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				sxCurr:0,
				sx_show:false
			}
		},
		methods: {
			
			change(i){
				const self = this;
				self.sxCurr = i
				if(i==3){
					self.sx_show = true
				}else{
					self.sx_show = false
				}
			},
			
			close(){
				const self = this;
				self.sx_show = false
			}
			
		}
	}
</script>

<style>
.sxIcon{width: 14rpx;height: 8rpx;}
.sxIcon1{width: 27rpx;height: 30rpx;}
.sx .item{width: 25%;position: relative;display: flex;justify-content: center;padding: 30rpx 0;}
.sx .item:nth-child(4)::before{content: '';width: 1px;height: 30rpx;background-color: #e1e1e1;position: absolute;left: 0;}

.w600{width: 600rpx;}
.sxCon{padding-bottom: 80rpx;}
.sxbg{background-color: #F8F4F5;}
.btn{line-height: 80rpx;height: 80rpx;}
.sx .sign{width: 174rpx;line-height: 92rpx;border-radius: 10rpx;background-color: #f5f5f5;text-align: center;margin: 20rpx 19rpx 0 0;}
.sx .sign:nth-child(3n){margin-right: 0;}
.sx .on{background-color: #F9F2E4;color: #E6B968;}
</style>
