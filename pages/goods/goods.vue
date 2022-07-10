<template>
	<view class="goods_list">
		<goods-list :goods="goodsmessage"></goods-list>
		<view class="isover" v-if="flag">----我是有底线的----</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				pageindex: 1,
				goodsmessage: [],
				flag:false
			}
		},
		onLoad() {
			this.getGoodslist()
		},
		methods: {
			async getGoodslist() {
				const res = await this.$myRequest({
					url: '/api/getgoods?pageindex=' + this.pageindex
				})
				this.goodsmessage = [...this.goodsmessage, ...res.data.message]
				
				
			}
		},
		components: {
			"goods-list": goodsList
		},
		onReachBottom() {
			if(this.goodsmessage.length<this.pageindex*10) return this.flag = true
			this.pageindex++;
			this.getGoodslist();
			
			
		},
		onPullDownRefresh() {
			this.pageindex=1
			this.goodsmessage=[]
			this.flag = false
			setTimeout(()=>{
				this.getGoodslist().then(()=>{uni.stopPullDownRefresh()})
			},1000)
		}
		
	}
</script>

<style lang="scss">
	.goods_list {
		background-color: #eee;
	}
	.isover{
		width: 100%;
		height: 50px;
		line-height: 50px;
		text-align: center;
		font-size: 28rpx;
		color: #22a076;
	}
</style>
