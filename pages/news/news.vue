<template>
	<view class="news">
		<news-item :list="news" @itemClick="goDetail"></news-item>
	</view>
</template>

<script>
	import newsItem from "../../components/news_item/news_item.vue"
	export default {
		data() {
			return {
				news:[]
			}
		},
		methods: {
			async getNews(){
				const res = await this.$myRequest({
					url: '/api/getnewslist'
				})
				this.news = res.data.message
				console.log(this.news);
			},
			goDetail(id){
				uni.navigateTo({
					url: '/pages/news-detail/news-detail?id='+id,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
				console.log(id);
			}
			
		},
		components: {"news-item":newsItem},
		onLoad() {
			this.getNews()
		}
	}
</script>

<style lang="scss">
	
</style>
