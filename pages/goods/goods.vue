<template>
	<view class="goods_list">
		<goods-list :goods="goodsmessage"></goods-list>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				pageindex: 1,
				goodsmessage:[]
			}
		},
		onLoad() {
			this.getGoodslist()
		},
		methods: {
			async getGoodslist() {
				const res = await this.$myRequest({
					url: '/api/getgoods?pageindex='+this.pageindex
				})
				this.goodsmessage = res.data.message
				
			}
		},
		components: {
			"goods-list": goodsList
		}
	}
</script>

<style lang="scss">
.goods_list{
	background-color: #eee;
}
</style>
