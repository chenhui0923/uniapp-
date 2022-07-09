<template>

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
</template>

<script>
	export default{
		props:['goods']
	}
</script>

<style lang="scss">
	.goods_list {
		padding: 0 15rpx;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		//防止tabbar导致的view遮盖
		padding-bottom: var(--window-bottom);

		.goods_item {
			background: #fff;
			width: 355rpx;
			margin: 10rpx 0;
			padding: 10rpx;

			box-sizing: border-box;

			image {
				width: 80%;
				height: 150px;
				margin: 0 auto;
				display: block;
			}

			.price {
				color: $shop-color;
				font-size: 36rpx;
				margin: 10rpx 0 5rpx 0;

				text:nth-child(2) {
					color: #ccc;
					font-size: 28rpx;
					margin-left: 7rpx;
					text-decoration: line-through;
				}
			}

			.shop_name {
				font-size: 28rpx;
				line-height: 50rpx;
				padding-bottom: 15rpx;
				padding-top: 10rpx;
			}
		}
	}
</style>
