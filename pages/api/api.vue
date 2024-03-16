<template>
	<view class="">
		<view class="nav">
			<u-navbar title="" @rightClick="rightClick" placeholder>
				<view slot="left" class="flex flex-row items-center">
					<u-icon name="list" color="#141414" size="26"></u-icon>
					<view class="ml-2 flex flex-col">
						<view class="text-sm">交易</view>
						<view class="text-base text-stone-500" style="color: #1756d5;">3.01 USD</view>
					</view>
				</view>
				<view slot="right" class="flex flex-row">
					<span class="iconfont icon-shuangxiangjiantou text-2xl ml-4"></span>

					<u-icon name="plus" class="ml-4" color="#141414" size="20"></u-icon>
				</view>
			</u-navbar>
		</view>
		<view class="cell flex justify-between items-center mt-2" style="color: #171717;font-weight: bold;"
			v-for="(it,index) in cellArr" :key="index">
			<view>{{it.txt}}</view>
			<u-line style="width: 60%;" color="#e5e5e5" :dashed="true" />
			<view :style="{color:it.color}">{{it.val}}</view>
		</view>
		<view class="cell flex justify-between items-center mt mt-2" style="font-weight: bold;height:70rpx">
			<view>价位：</view>
			<view class="flex flex-col items-end">
				<u-icon name="more-dot-fill" color="#989898" size="20"></u-icon>
			</view>
		</view>

		<view class="cell flex justify-between items-center pt-10 vm">
			<view class="flex flex-col items-start">
				<view>EURUSD, <span style="color: #1756d5;">buy 0.01</span></view>
				<view style="color: #787878;">1.08468 -> 1.08469</view>
			</view>
			<view class="flex flex-col items-end">
				<view style="color: #1756d5;">0.01</view>
			</view>
		</view>

		<view class="cell flex justify-between items-center pt-10 vm">
			<view class="flex flex-col items-start">
				<view>EURUSD, <span style="color: #1756d5;">buy 0.01</span></view>
				<view style="color: #787878;">1.08468 -> 1.08469</view>
			</view>
			<view class="flex flex-col items-end">
				<view style="color: #1756d5;">0.73</view>
			</view>
		</view>
	</view>
</template>

<script>
	const collection = "hello";
	export default {
		data() {
			return {
				name: "",
				cellArr: [{
					val: '999.96',
					color: '',
					txt: '结余:'
				}, {
					val: '1000.00',
					txt: '净值:'
				}, {
					val: '0.00',
					txt: '预付款:'
				}, {
					val: '0.00',
					txt: '可用预付款:'
				}, {
					val: '999.96',
					txt: '预付比例(%):'
				}]
			}
		},
		methods: {
		}
	}
</script>

<style scoped>
	.input {
		border: 1px solid #ebebeb;
		border-radius: 3px;
		margin-top: 15px;
		margin-bottom: 15px;
		padding: 8px;
	}

	.cell {
		padding: 0 24rpx;
	}

	.vm {
		padding-top: 20rpx;
		padding-bottom: 20rpx;
		color: #171717;
		font-weight: bold;
		border-top: 1px solid #e5e5e5;
	}

	.mt {
		border-top: 1px solid #e5e5e5;
		background-color: #f7f7f7;
		color: #989898;
	}
</style>