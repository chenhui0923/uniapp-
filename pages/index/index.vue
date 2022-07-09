<template>
	<view class="home">
		<swiper indicator-dots autoplay circular>
			<swiper-item v-for="item in swipers" :key="item.id">
				<image :src="item.img"></image>
			</swiper-item>

		</swiper>
		<!-- 导航 -->
		<view class="nav">
			<view class="nav_item" v-for="(item,index) in navs" :key="index" @click="navClik(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.title}}</text>
			</view>
		</view>
		<!-- 推荐商品 -->
		<view class="hot_goods">
			<view class="tit">推荐商品</view>
			<view class="goods_list">
				
				<view class="goods_item" v-for="good in goods" :key="good.id">
					<image :src="good.img_url"></image>
					<view class="price">
						<text>￥{{good.sell_price}}</text>
						<text>￥{{good.market_price}}</text>
					</view>
					<view class="shop_name">
					  {{good.title}}
					</view>
				</view>
			
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swipers: [],
				goods:[],
				navs:[
					{
						icon:'iconfont icon-fuwuchaoshi',
						title:'垃圾超市',
						path:'/pages/goods/goods'
					},
					{
						icon:'iconfont icon-lianxi',
						title:'联系我们',
						path:'/pages/contact/contact'
					},
					{
						icon:'iconfont icon-shequ',
						title:'社区图片',
						path:'/pages/pics/pics'
					},
					{
						icon:'iconfont icon-shouye',
						title:'学习视频',
						path:'/pages/video/video'
					}
				]
			}
		},
		onLoad() {
			this.getSwipers()
			this.getHotGoods()
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
			},
			async getHotGoods(){
			const res = await this.$myRequest({
					url:'/api/getgoods?pageindex=1'
				})
				// console.log(res);
				this.goods = res.data.message
				console.log(this.goods);
			},
			navClik(url){
				uni.navigateTo({
					url: url,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
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

	.nav {
		display: flex;

		.nav_item {
			width: 25%;
			text-align: center;
			font-size: 30rpx;

			view {
				width: 120rpx;
				height: 120rpx;
				background:$shop-color;
				border-radius: 60rpx;
				margin: 10rpx auto;
				line-height: 120rpx;
				color: #fff;
				font-size: 55rpx;
			}

			.icon-lianxi {
				font-size: 60rpx;
				line-height: 125rpx;
			}

			.icon-shouye {
				line-height: 125rpx;

			}
		}
	}

	.hot_goods {
		
		background-color: #eee;
		// overflow解决外边距塌陷：如果给子元素添加margin-top样式,父级元素也会跟着下来，造成外边距塌陷
		overflow:hidden;
		margin-top: 10rpx;
		.tit {
			height: 50px;
			line-height: 50px;
			color:$shop-color;
			text-align: center;
			background-color: #fff;
			letter-spacing: 20px;
			margin: 7rpx 0;
		}
	}
	.goods_list{
		padding: 0 15rpx;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		//防止tabbar导致的view遮盖
		padding-bottom: var(--window-bottom);
		.goods_item{
			background: #fff;
			width: 355rpx;
			margin: 10rpx 0;
			padding: 10rpx;
			
			box-sizing: border-box;
			
			image{
				width: 80%;
				height: 150px;
				margin: 0 auto;
				display: block;
			}
			.price{
				color: $shop-color;
				font-size: 36rpx;
				margin: 10rpx 0 5rpx 0  ;
				text:nth-child(2){
					color: #ccc;
					font-size: 28rpx;
					margin-left: 7rpx;
					text-decoration: line-through;
				}
			}
			.shop_name{
				font-size: 28rpx;
				line-height: 50rpx;
				padding-bottom: 15rpx;
				padding-top: 10rpx;
			}
		}
	}
</style>
