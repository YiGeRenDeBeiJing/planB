<template>
	<view>
		<view class="nav">
			<u-navbar title="" autoBack @rightClick="rightClick" placeholder>
				<view slot="left" class="flex flex-row items-center">
					<u-icon name="arrow-left" color="#141414" size="18"></u-icon>
					<view class="ml-2 flex flex-col">
						<view class="text-base">EURUSD</view>
						<view class="text-sm text-stone-500">EMO VS US Dollar</view>
					</view>
				</view>
				<view slot="right" class="flex flex-row">
					<u-icon name="search" color="#141414" size="26"></u-icon>
				</view>
			</u-navbar>
		</view>
		<u-cell-group :title="it.title" v-for="(it,index) in cellArr" :key="'g'+index">
			<u-cell :title="its.txt" :value="its.val" :border="false" v-for="(its,ids) in it.children"
				:key="'c'+ids" :class="its.border?'borderLeft':''">
				<view slot="value" v-if="its.type == 'switch'">
					<u-switch v-model="its.switchval" size="20"></u-switch>
				</view>
			</u-cell>
		</u-cell-group>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				titles: '',
				cellArr: [{
						title: '属性',
						children: [{
							txt: '部门',
							val: 'currency'
						}, {
							txt: '小数位',
							val: '5'
						}, {
							txt: '合约数量',
							val: '100000'
						}, {
							txt: '点差',
							val: '浮动'
						}, {
							txt: '止损水平',
							val: '0'
						}, {
							txt: '预付款货币',
							val: 'EUR'
						}, {
							txt: '利润货币',
							val: 'USD'
						}, {
							txt: '计算',
							val: 'Forex'
						}, {
							txt: '锁仓预付款',
							val: '100000'
						}, {
							txt: '利润货币',
							val: 'USD'
						}, {
							txt: '交易',
							val: '完全交易'
						}, {
							txt: '操作',
							val: '即使执行'
						}, {
							txt: '直到取消模式',
							val: '直到取消'
						}, {
							txt: '成交指令',
							val: '全部或取消'
						}, {
							txt: '超期',
							val: '所有'
						}, {
							txt: '订单',
							val: '所有'
						}, {
							txt: '最小量',
							val: '0.01'
						}, {
							txt: '最大量',
							val: '500'
						}, {
							txt: '交易量步长',
							val: '0.01'
						}, {
							txt: '库存费类型',
							val: '点模式'
						}, {
							txt: '买入库存费',
							val: '-0.7'
						}, {
							txt: '卖出库存费',
							val: '=1'
						}, {
							txt: '订阅',
							val: '实时价格Level 2'
						}, ]
					},
					{
						title: '库存费系数',
						children: [{
							txt: '星期一',
							val: '1'
						},{
							txt: '星期二',
							val: '1'
						},{
							txt: '星期三',
							val: '3'
						},{
							txt: '星期四',
							val: '1'
						},{
							txt: '星期五',
							val: '1'
						}, ]
					},
					{
						title:'预付款率：初始推荐',
						children:[{
							txt:'显示该货币值，USD 每手',
							val:'',
							type:'switch',
							switchval:true
						},{
							txt: '类型',
							val: '浮动，每个交易品种的名义价值，USD'
						},{
							txt: '市场买入',
							val: ''
						},{
							txt: '0-300 000',
							val: '~ 1085.48 / ~ 1085.48',
							border:1
						},{
							txt: '300 000 - 500 000',
							val: '~ 2170.96 / ~ 2170.96',
							border:1
						},{
							txt: '500 000 - 10 000 0',
							val: '~ 3256.41 / ~ 3256.41',
							border:1
						},{
							txt: '市场卖出',
							val: ''
						},{
							txt: '0-300 000',
							val: '~ 1085.48 / ~ 1085.48',
							border:1
						},{
							txt: '300 000 - 500 000',
							val: '~ 2170.96 / ~ 2170.96',
							border:1
						},{
							txt: '500 000 - 10 000 0',
							val: '~ 3256.41 / ~ 3256.41',
							border:1
						},{
							txt: '',//勿删，占位
							val: ''
						},]
					},
					{
						title: '行情交易期间',
						children: [{
							txt: '星期日',
							val: ''
						},{
							txt: '星期一',
							val: '00:00:00-24:00:00'
						},{
							txt: '星期二',
							val: '00:00:00-24:00:00'
						},{
							txt: '星期三',
							val: '00:00:00-24:00:00'
						},{
							txt: '星期四',
							val: '00:00:00-24:00:00'
						},{
							txt: '星期五',
							val: '00:00:00-24:00:00'
						}, {
							txt: '星期六',
							val: ''
						},]
					},
					{
						title: '交易期间',
						children: [{
							txt: '星期日',
							val: ''
						},{
							txt: '星期一',
							val: '00:00:00-24:00:00'
						},{
							txt: '星期二',
							val: '00:00:00-24:00:00'
						},{
							txt: '星期三',
							val: '00:00:00-24:00:00'
						},{
							txt: '星期四',
							val: '00:00:00-24:00:00'
						},{
							txt: '星期五',
							val: '00:00:00-24:00:00'
						}, {
							txt: '星期六',
							val: ''
						},]
					},
				]
			}
		},
		onLoad(q) {
			this.titles = q.name
		},
		methods: {

		}
	}
</script>

<style lang="scss" scoped>
	/deep/ {
		.u-cell-group__title {
			background: #f7f7f7;
		}

		.u-cell__title-text,
		.u-cell__value {
			font-size: 16rpx !important;
			padding: 0 14rpx;
		}
		.u-cell__value{
			color: #888;
		}

		.u-cell__body {
			margin: 0;
			padding:  0;
		}
		.u-cell{
			margin: 10rpx 30rpx;
		}
		.borderLeft{
			border-left: 1px solid #bababa;
			width: 80%;
			margin-left: 10%;
			margin-top: 0;
			margin-bottom: 0;
		}
	}
</style>