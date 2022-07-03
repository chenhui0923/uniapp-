<template>
	<view class="home">
		<swiper indicator-dots autoplay circular>
			<swiper-item v-for="item in swipers" :key="item.id">
				<image :src="item.img"></image>
			</swiper-item>

		</swiper>
		<!-- 导航 -->
		<view class="nav">
			<view class="nav_item">
				<view class="iconfont icon-fuwuchaoshi"></view>
				<text>垃圾超市</text>
			</view>
			<view class="nav_item">
				<view class="iconfont icon-lianxi"></view>
				<text>联系我们</text>
			</view>
			<view class="nav_item">
				<view class="iconfont icon-shequ"></view>
				<text>社区图片</text>
			</view>
			<view class="nav_item">
				<view class="iconfont icon-shouye"></view>
				<text>学习视频</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swipers: []
			}
		},
		onLoad() {
			this.getSwipers()
		},
		methods: {
			async getSwipers() {
				// console.log('获取轮播图');
				// uni.request({
				// 	url: 'http://localhost:8082/api/getlunbo',
				// 	method: 'GET',
				// 	data: {},
				// 	success: res => {
				// 		console.log(res);
				// 		if(res.data.status !== 0 ){
				// 			return uni.showToast({
				// 				title: '获取数据失败'
				// 			});
				// 		}
				// 		this.swipers = res.data.message
				// 		console.log(this.swipers);
				// 	},
				// 	fail: () => {},
				// 	complete: () => {}
				// });
				const res = await this.$myRequest({
					url: '/api/getlunbo'
				})

				this.swipers = res.data.message
				console.log(this.swipers);
			}
		}
	}
</script>

<style lang="scss">
	.home {
		width: 750rpx;
		height: 380rpx;

		image {
			height: 100%;
			width: 100%;
		}
	}
	.nav{
		display: flex;
		.nav_item{
			width: 25%;
			text-align: center;
			font-size: 30rpx;
			view{
				width: 120rpx;
				height: 120rpx;
				background: #d81e1e;
				border-radius: 60rpx;
				margin: 10rpx auto;
				line-height: 120rpx;
				color: #fff;
				font-size: 55rpx;
			}
			.icon-lianxi{
				font-size: 60rpx;
				line-height: 125rpx;
			}
			.icon-shouye{
				line-height: 125rpx;
		
			}
		}
	}
</style>
