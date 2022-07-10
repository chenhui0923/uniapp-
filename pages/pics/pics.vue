<template>
	<view class="pics">
		<scroll-view class="left">
			<view>家具生活</view>
			<view>家具生活</view>
			<view>家具生活</view>
			<view>家具生活</view>
			<view>家具生活</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cates:[]
			}
		},
		methods: {
			async getPicsCate () {
				const res = await this.$myRuquest({
					url: '/api/getimgcategory'
				})
				this.cates = res.data.message
				this.leftClickHandle(0,this.cates[0].id)
			},
		}
	}
</script>

<style lang="scss">
	.pics{
		height: 100%;
		display: flex;
		.left{
			width: 200rpx;
			height: 100%;
			border-right:1px solid #eee;
			view{
				height: 60px;
				line-height: 60px;
				color: #333;
				text-align: center;
				font-size: 30rpx;
				border-top:1px solid #eee;
			}
			.active{
				background: $shop-color;
				color: #fff;
			}
		}
		.right{
			height: 100%;
			width: 520rpx;
			margin: 10rpx auto;
			.item{
				image{
					width: 520rpx;
					height: 520rpx;
					border-radius: 5px;
				}
				text{
					font-size: 30rpx;
					line-height: 60rpx;
				}
			}
		}
	}
</style>
