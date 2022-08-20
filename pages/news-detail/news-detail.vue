<template>
	<view class="news_detail">
		<text class="handtitle">{{data.title}}</text>
		<view class="info">
			<text>发表时间：{{data.add_time| formatDate}}</text>
			<text>浏览次数：{{data.click}}</text>
		</view>
		<view class="content">
			<rich-text :nodes="data.content"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				newsid:0,
				data:[]
			}
		},
		methods: {
			async getNewsDetail(){
				const res = await this.$myRequest({
					url:'/api/getnew/'+this.newsid,
				})
				this.data = res.data.message[0]
				console.log(this.data);
			}
		},
		onLoad(option) {
			console.log(option);
			this.newsid= option.id
			this.getNewsDetail()
		}
		
	}
</script>

<style lang="scss">
	.news_detail{
		font-size:30rpx;
		padding: 0 20rpx;
		.handtitle{
			font-size: 45rpx;
			text-align: center;
			width:auto;
			display: block;
			margin: 20rpx 0;
		}
		.info{
			display: flex;
			justify-content: space-between;//首尾分布均匀
			margin: 15rpx 0;
		}
	}
</style>
