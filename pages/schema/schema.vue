<template>
	<view class="">
		<view class="nav">
			<u-navbar title="" @rightClick="rightClick" placeholder>
				<view slot="left" class="flex flex-row items-center">
					<u-icon name="list" color="#141414" size="26"></u-icon>
					<view class="ml-2 flex flex-col">
						<view class="text-sm">历史</view>
						<view class="text-base text-stone-500">全部交易品种</view>
					</view>
				</view>
				<view slot="right" class="flex flex-row">
					<span class="iconfont icon-money text-2xl"></span>
					<span class="iconfont icon-shuangxiangjiantou text-2xl ml-4"></span>
					<span class="iconfont icon-rili text-2xl ml-4"></span>
				</view>
			</u-navbar>
		</view>
		<u-tabs class="mt-2" :list="list" :scrollable="false" :current="current" @change="change"></u-tabs>
		<view class="cell flex justify-between items-center mt-2" style="color: #171717;font-weight: bold;"
			v-for="(it,index) in cellArr" :key="index">
			<view>{{it.txt}}</view>
			<u-line style="width: 70%;" color="#e5e5e5" :dashed="true" />
			<view :style="{color:it.color}">{{it.val}}</view>
		</view>
		<view class="mt-4"><u-line class="mt-2" style="width: 100%;" color="#e5e5e5" /></view>
		<view class="cell flex justify-between items-center mt-2" style="color: #171717;font-weight: bold;">
			<view class="text-lg">结余：</view>
			<view class="flex flex-col items-end">
				<view style="color: #787878;">2024.03.29 16:22:22</view>
				<view style="color: #1756d5;">1000.00</view>
			</view>
		</view>

		<view class="cell flex justify-between items-center pt-10 vm mt-2"
			:style="{'border-left':'16rpx solid green'}">
			<view class="flex flex-col items-start">
				<view>EURUSD, <span style="color: #1756d5;">buy 0.01</span></view>
				<view style="color: #787878;">1.08468 -> 1.08469</view>
			</view>
			<view class="flex flex-col items-end">
				<view style="color: #787878;">2024.03.29 16:22:22</view>
				<view style="color: #1756d5;">0.01</view>
			</view>
		</view>

		<view class="cell flex justify-between items-center pt-10 vm"
			:style="{'border-left':'16rpx solid orange'}">
			<view class="flex flex-col items-start">
				<view>EURUSD, <span style="color: #1756d5;">buy 0.01</span></view>
				<view style="color: #787878;">1.08468 -> 1.08469</view>
			</view>
			<view class="flex flex-col items-end">
				<view style="color: #787878;">2024.03.29 16:22:22</view>
				<view style="color: #8b142b;">-0.04</view>
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
				list: [{
					name: '待收货'
				}, {
					name: '待付款'
				}, {
					name: '待评价',
					count: 5
				}],
				current: 0,
				cellArr: [{
					val: '-0.04',
					color: '#8b142b',
					txt: '利润:'
				}, {
					val: '1000.00',
					txt: '入金:'
				}, {
					val: '0.00',
					txt: '库存费:'
				}, {
					val: '0.00',
					txt: '手续费:'
				}, {
					val: '999.96',
					txt: '结余:'
				}]
			}
		},
		methods: {
			change() {

			}
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
</style>