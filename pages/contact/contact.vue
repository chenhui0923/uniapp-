<template>
	<view class="contact">
		<image class="contactimg" src="http://www.itcast.cn/2018czydz/images/gywmban.jpg"></image>
		<view class="info">
			<text @click="phone">联系电话：13276040802( 点击拨打 )</text>
			<view>地址：我是家在月球，不要想找到我</view>
		</view>
		<map class="map" :longitude="longitude" :scale="scale" :latitude="latitude" :markers="markers" enable-traffic="true"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude:119.268384 ,
				latitude: 26.05017,
				scale: 13,
				markers: [{
					longitude: 119.268384,
					latitude:  26.05017,
					iconPath: '../../static/logo.png',
					width: 30,
					height: 30
				}]
			}
		},
		methods: {
			phone() {

				uni.makePhoneCall({
					
					phoneNumber: '13276040802'
				})
				console.log(this.phoneNumber);
			}
		}
	}
</script>

<style lang="scss">
	.contact {
		.contactimg {
			width: 750rpx;
			height: 320rpx;
		}

		.info {
			padding: 10rpx 20rpx;
			font-size: 30rpx;

			view {
				line-height: 80rpx;
				border-bottom: 1px solid #eee;
			}
		}

		.map {
			width: 750rpx;
			height: 750rpx;
		}
	}
</style>
