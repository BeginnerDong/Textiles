<template>
	<view>
		
		<view class="p-3 flex1">
			<view class="flex font-24 color8 px-3 mr-3 b-e1 flex-1 ss">
				<image src="../../static/images/home-icon.png" class="wh36 mr-3"></image>
				<input type="text" v-model="keywords" placeholder="搜索想要找的商品" />
			</view>
			<view class="font-30 colorM font-w" @click="search()">搜索</view>
		</view>
		
		
		<view class="flex1 px-3 pb-3" v-for="(item,index) in mainData" :key="index"
		:data-id="item.id"
		@click="Router.navigateTo({route:{path:'/pages/goodDetail/goodDetail?id='+$event.currentTarget.dataset.id}})">
			<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="listImg"></image>
			<view class="flex5 font-30 py-0 flex-1 pl-2 h213">
				<view class="avoidOverflow2">{{item.title?item.title:''}}</view>
				<view class="flex1">
					<view class="price1 font-32 font-w">{{item.price?item.price:''}}</view>
					<image src="../../static/images/classification-icon3.png" class="wh52"></image>
				</view>
			</view>
		</view>
		
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mainData:[],
				searchItem:{
					type:1
				}
			}
		},
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			
		},
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		methods: {
			
			search(){
				const self = this;
				if(self.keywords==''){
					self.$Utils.showToast('请输入关键词搜索', 'none');
				}else{
					self.searchItem.title = ['LIKE',['%'+self.keywords+'%']]
					self.getMainData(true)
				}
			},
			
			getMainData(isNew) {
				const self = this;
				if(isNew){
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage:1,
						pagesize:10,
						is_page:true,
					}
				};
				const postData = {};
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem)
				postData.getAfter = {
					sku:{
						tableName:'Sku',
						middleKey:'product_no',
						key:'product_no',
						searchItem:{
							status:1
						},
						condition:'='
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					} else {
						self.$Utils.showToast('没有更多了', 'none');
					};
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.productGet(postData, callback);
			},
				
		}
	}
</script>

<style scoped>

</style>
