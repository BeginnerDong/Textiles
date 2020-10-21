<template>
	<view>
		
		<view class="p-s top-0 bg-white z10 pt-3">
			<view class="flex font-24 color8 px-3 mx-3 b-e1 flex-1 ss" @click="Router.navigateTo({route:{path:'/pages/search/search'}})">
				<image src="../../static/images/home-icon.png" class="wh36 mr-3"></image>
				<input type="text" disabled="true" placeholder="搜索想要找的商品" />
			</view>
			<view class="font-30 color8 line-h bB-e1 flex1 mb-3 sx">
				<view class="item" @click="changeOrder('defalut')" :class="!order.sale_count&&!order.price?'colorM':''">综合</view>
				<view class="item" @click="changeOrder('sale_count')" :class="order.sale_count?'colorM':''">销量</view>
				<view class="flex item" @click="changeOrder('price')" :class="order.price?'colorM':''">
					<view>价格</view>
					<view class="pl-1">
						<image :src="order.price&&order.price=='asc'?'../../static/images/classification-icon1-a.png':'../../static/images/classification-icon1.png'" class="sxIcon mb-1"></image>
						<image :src="order.price&&order.price=='desc'?'../../static/images/classification-icon2-a.png':'../../static/images/classification-icon2.png'" class="sxIcon"></image>
					</view>
				</view>
				<view class="flex item" @click="change(3)" :class="searchItem.brand||searchItem.category_id?'colorM':''">
					<view>筛选</view>
					<image src="../../static/images/classification-icon.png" class="sxIcon1 ml-1"></image>
				</view>
			</view>
		</view>
		
		<!-- 搜索结果 -->
		<view class="flex1 px-3 pb-4" v-for="(item,index) in mainData" :key="index"
		>
			<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="listImg" :data-id="item.id"
		@click="Router.navigateTo({route:{path:'/pages/goodDetail/goodDetail?id='+$event.currentTarget.dataset.id}})"></image>
			<view class="flex5 font-30 py-0 flex-1 pl-2 h213">
				<view class="avoidOverflow2" :data-id="item.id"
		@click="Router.navigateTo({route:{path:'/pages/goodDetail/goodDetail?id='+$event.currentTarget.dataset.id}})">{{item.title?item.title:''}}</view>
				<view class="flex1">
					<view class="price1 font-32 font-w">{{item.price?item.price:''}}</view>
					<view  class="font-24 color6">已售：{{item.sale_count?item.sale_count:0}}</view>
					<image @click="addCar(index)" src="../../static/images/classification-icon3.png" class="wh52"></image>
				</view>
			</view>
		</view>
		
		<!-- 筛选弹框 -->
		<view class="bg-mask" v-show="sx_show">
			<view class="w600 bg-white p-aY right-0 font-24 line-h flex5 sx">
				<view class="sxbg p-2 pt-3">筛选</view>
				<view class="flex-1 flexY sxCon">
					<view class="p-2 mt-1 bB-f5">
						<view>品牌</view>
						<view class="flex flex-wrap">
							<view class="sign"  v-for="(item,index) in brandData" :key="index"
							:class="Utils.inArray(item.id,chooseBrand)!=-1?'on':''"
							@click="chooseBrandItem(index)"
							>{{item.title}}</view>
						</view>
					</view>
					<view class="p-2 mt-1 bB-f5">
						<view>类别</view>
						<view class="flex flex-wrap">
							<view class="sign" v-for="(item,index) in labelData" :key="index"
							:class="Utils.inArray(item.id,chooseLabel)!=-1?'on':''"
							@click="chooseLabelItem(index,'brand')"
							>{{item.title}}</view>
						</view>
					</view>
				</view>
				
				<view class="p-aX bottom-0 flex colorf">
					<view class="btn w-50 bg3c" @click="reset">重置</view>
					<view class="btn w-50 Mgb" @click="confirm">确定</view>
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
				sx_show:false,
				mainData:[],
				order:{},
				searchItem:{
					status:1,
					type:1
				},
				keywords:'',
				brandData:[],
				labelData:[],
				chooseLabel:[],
				chooseBrand:[],
				Utils:this.$Utils,
			}
		},
		onLoad(options) {
			const self = this;
			if(options.brandId){
				self.chooseBrand.push(parseInt(options.brandId));
				self.searchItem.brand = ['in',self.chooseBrand]
			};
			console.log('self.chooseBrand',self.chooseBrand)
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData','getBrandData','getLabelData'], self);
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
			
			addCar(index) {
				const self = this;
				if(!self.mainData[index].sku[0]){
					uni.setStorageSync('canClick',true);
					self.$Utils.showToast('暂无可选规格', 'none');
					return
				};
				var obj = self.mainData[index];
				obj.skuIndex = 0;
				obj.skuId = self.mainData[index].sku[0].id;
				var array = self.$Utils.getStorageArray('cartData');
				for (var i = 0; i < array.length; i++) {
					if (array[i].skuId == self.mainData[index].sku[0].id) {
						var target = array[i]
					}
				};
				console.log(target)
				if (target) {
					target.count = target.count + 1
				} else {
					console.log(111)
					var target = self.mainData[index];
					target.count = 1;
					target.isSelect = true;
				}
				self.$Utils.showToast('加入购物车成功', 'none');
				self.$Utils.setStorageArray('cartData', target, 'skuId', 999);
			},
			
			chooseBrandItem(index) {
				const self = this;
				var position = self.chooseBrand.indexOf(self.brandData[index].id);
				if (position >= 0) {
					self.chooseBrand.splice(position, 1);
				} else {
					self.chooseBrand.push(self.brandData[index].id);
				};
				console.log('self.chooseBrand',self.chooseBrand)
			},
			
			chooseLabelItem(index) {
				const self = this;
				var position = self.chooseLabel.indexOf(self.labelData[index].id);
				if (position >= 0) {
					self.chooseLabel.splice(position, 1);
				} else {
					self.chooseLabel.push(self.labelData[index].id);
				};
			},
			
			confirm(){
				const self = this;
				if(self.chooseBrand.length>0){
					self.searchItem.brand = ['in',self.chooseBrand]
				}else{
					delete self.searchItem.brand
				}
				if(self.chooseLabel.length>0){
					self.searchItem.category_id = ['in',self.chooseLabel]
				}else{
					delete self.searchItem.category_id
				};
				self.sx_show = false;
				self.getMainData(true)
			},
			
			reset(){
				const self = this;
				self.chooseBrand = [];
				self.chooseLabel = []
			},
			
			getLabelData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					type: 3,
					id:['not in',[4]]
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.labelData = res.info.data
					}
					self.$Utils.finishFunc('getLabelData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			getBrandData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					type: 2
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.brandData = res.info.data
					}
					self.$Utils.finishFunc('getBrandData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			search(){
				const self = this;
				if(self.keywords==''){
					self.$Utils.showToast('请输入关键词搜索', 'none');
				}else{
					self.searchItem.title = ['LIKE',['%'+self.keywords+'%']]
					self.getMainData(true)
				}
			},
			
			changeOrder(type){
				const self = this;
				if(type=='defalut'){
					self.order = {}
				}else if(type=='sale_count'){
					self.order = {sale_count:'desc'}
				}else if(type=='price'){
					if(self.order[type]){
						if(self.order[type]=='desc'){
							
							self.order = {price:'asc'}
						}else{
							self.order = {price:'desc'}
						}
					}else{
						self.order = {price:'desc'}
					}
				};
				self.getMainData(true)
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
				if(JSON.stringify(self.order)!="{}"){
					postData.order = self.$Utils.cloneForm(self.order)
				};
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
