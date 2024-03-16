<template>
	<view class="set-content">
		<view class="nav">
			设置
		</view>
		<button type="button" class="group current svelte-1kgzcsm">
			<view class="name svelte-1kgzcsm">MetaTrader Web</view>
			<view class="info svelte-1kgzcsm">10001166819 - MetaQuotes</view>
			<view class="tag demo svelte-1s63r9n" title="模拟">模拟</view>
		</button>
		<view class="cell flex justify-between items-center" v-for="(it,index) in cellArr" :key="index" :style="{'border-bottom':it.botton?'2rpx solid #e8e8e8':''}" @click="cellClick(it)">
			<image class="flex items-center justify-center" :src="it.url" mode=""></image>
			<view>{{it.text}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cellArr:[{
					url:"../../static/set/act9u-1k5e5.png",
					text:'交易账号'
				},{
					url:"../../static/set/azwxq-zmdiq.png",
					text:'账户充值'
				},{
					url:"../../static/set/asnds-tuszj.png",
					text:'账户提现',
					botton:1
				},{
					url:"../../static/set/awjna-67n71.png",
					text:'深蓝主题'
				},{
					url:"../../static/set/a6qws-bdsvm.png",
					text:'颜色模板',
					botton:1
				},{
					url:"../../static/set/ac3iw-4n8nm.png",
					text:'单击交易'
				},{
					url:"../../static/set/azl2s-t1al1.png",
					text:'MetaTrader 5'
				},{
					url:"../../static/set/anxey-52fj5.png",
					text:'经济日历',
					botton:1
				},{
					url:"../../static/set/anql3-2spqm.png",
					text:'日志'
				},{
					url:"../../static/set/az21x-dhfa2.png",
					text:'语言'
				},{
					url:"../../static/set/ae0l9-8oqt8.png",
					text:'第三方聊天接口'
				},{
					url:"../../static/set/ay6ej-4hjx6.png",
					text:'关于我们'
				}]
			};
		},
		methods:{
			cellClick(it){
				if(it.text == '账户充值'){
					uni.navigateTo({
						url:'/pages/recharge/recharge'
					})
				}
				if(it.text == '交易账号'){
					uni.navigateTo({
						url:'/pages/account/account'
					})
				}
				if(it.text == '账户提现'){
					uni.navigateTo({
						url:'/pages/withdrawal/withdrawal'
					})
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.set-content {
		padding: 0px 8rpx;

		.nav {
			display: flex;
			justify-content: center;
			align-items: center;
			height: 100rpx;
			background-color: var(--color-background);
			border-bottom: 2rpx solid var(--color-border);
			flex-basis: var(--m-screen-header-height);
			font-size: var(--font-big);
			height: var(--m-screen-header-height);
			padding: 0 var(--indent-half);
			justify-content: space-around;
			width: 100%;
			position: sticky;
			top: 0;
			z-index: 999;
		}

		.group.svelte-1kgzcsm:not(:last-child) {
			border-bottom: 2rpx solid var(--color-border);
			width: 100%;
		}

		.current.svelte-1kgzcsm,
		.name.svelte-1kgzcsm {
			overflow: hidden;
		}

		.current.svelte-1kgzcsm {
			color: var(--color-icon-default);
			min-height: calc(var(--indent)* 9);
			padding: 0 var(--indent2);
			flex-direction: column;
			justify-content: center;
			display: flex;
			position: relative;
			margin-bottom: 0;
			background: #fff;
			
			&::after{
				border: 0;
				border-bottom: 2rpx solid var(--color-border);
			}
			view {
				text-align: left;
			}
		}

		.name.svelte-1kgzcsm {
			text-overflow: ellipsis;
			white-space: nowrap;
			max-width: 500rpx;
			padding-bottom: 8rpx;
			font-size: 32rpx;
			height: 50rpx;
			line-height: 50rpx;
		}

		.info.svelte-1kgzcsm {
			font-size: var(--font-tiny);
			line-height: 32rpx;
		}

		.tag.demo.svelte-1s63r9n {
			background-color: var(--color-fill-greenHover);
			top: 20rpx;
			right: -80rpx;
		}

		.tag.svelte-1s63r9n {
			color: var(--color-text-inverted);
			height: var(--indent2);
			text-shadow: 2rpx 0 #6e6e6e, -2rpx 0 #6e6e6e, 0 2rpx #6e6e6e, 0 -2rpx #6e6e6e, 2rpx 2rpx #6e6e6e, -2rpx -2rpx #6e6e6e, 2rpx -2rpx #6e6e6e, -2rpx 2rpx #6e6e6e;
			justify-content: center;
			align-items: center;
			width: 240rpx;
			font-size: 18rpx;
			font-weight: 700;
			display: flex;
			position: absolute;
			transform: rotate(45deg);
		}
		.cell{
			padding: 0 var(--indent2);
			height: 96rpx;
			image{
				width: 48rpx;
				height: 48rpx;
			}
			view{
				width: 580rpx;
				margin-top: -5rpx;
			}
		}
	}
</style>