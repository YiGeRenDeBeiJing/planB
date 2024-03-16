<template>
	<view>
		<view class="nav">
			<u-navbar title="" @rightClick="rightClick" :autoBack="true" leftIcon="list" leftIconSize="26" leftText="行情"
				placeholder>
				<view slot="right" class="flex flex-row">
					<u-icon name="plus" color="#141414" size="20"></u-icon>
					<u-icon class="ml-4" name="edit-pen" color="#141414" size="26"></u-icon>
				</view>
			</u-navbar>
		</view>

		<view class="cell flex justify-between items-center mt-2" @click="cellClick('EURUSD')">
			<view class="left flex flex-col gray">
				<view class="text-sm mb-2">-9 <span class="ml-3 blue01">-0.01%</span></view>
				<view class="text-lg font-bold mb-2 black">EURUSD</view>
				<view class="text-sm">11:37:14 <span class="ml-3 mr-3">=></span>1</view>
			</view>
			<view class="right flex justify-between">
				<view class="flex flex-col">
					<view class="flex flex-row items-center text-lg blue mb-1">
						1.0853 <span class="text-2xl font-bold" style="margin-top: -4rpx;">84²</span>
					</view>
					<view class="text-sm indent-2 gray">L: 1.08415</view>
				</view>
				<view class="flex flex-col ">
					<view class="flex flex-row items-center text-lg blue mb-1">
						1.0853 <span class="text-2xl font-bold" style="margin-top: -4rpx;">84²</span>
					</view>
					<view class="text-sm indent-2 gray">H: 1.08415</view>
				</view>
			</view>
		</view>

		<view class="cell flex justify-between items-center" @click="cellClick('GBPUSD')">
			<view class="left flex flex-col gray">
				<view class="text-sm mb-2">-9 <span class="ml-3 red01">-0.01%</span></view>
				<view class="text-lg font-bold mb-2 black">GBPUSD</view>
				<view class="text-sm">11:37:14 <span class="ml-3 mr-3">=></span>1</view>
			</view>
			<view class="right flex justify-between">
				<view class="flex flex-col">
					<view class="flex flex-row items-center text-lg red mb-1">
						1.0853 <span class="text-2xl font-bold" style="margin-top: -4rpx;">84²</span>
					</view>
					<view class="text-sm indent-2 gray">L: 1.08415</view>
				</view>
				<view class="flex flex-col ">
					<view class="flex flex-row items-center text-lg red mb-1">
						1.0853 <span class="text-2xl font-bold" style="margin-top: -4rpx;">84²</span>
					</view>
					<view class="text-sm indent-2 gray">H: 1.08415</view>
				</view>
			</view>
		</view>
		<u-popup :show="show" closeOnClickOverlay @close="show = false">
			<view>
				<view class="poptitle flex flex-row items-center">{{currentMod.name}}: Euro vs Dolliar</view>
				<view class="popcell flex flex-row items-center" v-for="(it,index) in popArr" :key="index" @click="popcellClick(it)">{{it}}</view>
				<view class="popcell" style="height: 50rpx;"></view>
			</view>
		</u-popup>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				show:false,
				currentMod:{
					name:''
				},
				popArr:['新订单','图表','属性','市场深度','市场统计','简单视图模式']
			};
		},
		methods:{
			cellClick(m){
				this.currentMod.name = m
				this.show = !this.show
			},
			popcellClick(it){
				if(it == '属性'){
					uni.navigateTo({
						url:'/pages/hangqing/details?name='+this.currentMod.name
					})
				}
				if(it == '简单视图模式'){
					uni.navigateTo({
						url:'/pages/jdviews/jdviews?name='+this.currentMod.name
					})
				}
				this.show = false
			}
		}
	}
</script>

<style lang="scss" scoped>
	.nav {
		position: sticky;
		top: 0;
	}

	/deep/ {
		.u-navbar__content__left__text {
			font-size: 36rpx;
		}
	}

	.cell {
		height: 162rpx;
		padding: 0 30rpx;

		.left {
			width: 46%;
		}

		.right {
			width: 54%;
		}

		.blue {
			color: #1a55ad;
		}

		.blue01 {
			color: #225072;
		}

		.red {
			color: #d11009;
		}

		.red01 {
			color: #941e2f;
		}

		.gray {
			color: #888;
		}

		.black {
			color: #181717;
		}
	}
	.poptitle{
		height: 100rpx;
		padding: 0 20rpx;
		color: #7f7f77;
	}
	.popcell{
		height: 90rpx;
		padding: 0 20rpx;
	}
</style>