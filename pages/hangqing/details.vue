<template>
	<view>
		<view class="nav">
			<u-navbar title="" @rightClick="rightClick" :autoBack="true" leftIconSize="26" :leftText="titles"
				placeholder>
				<view slot="right" class="flex flex-row">
					<u-icon name="search" color="#141414" size="26"></u-icon>
				</view>
			</u-navbar>
		</view>
		<u-cell size="large" :title="it.title" value="1.08548" :border="false" v-for="(it,index) in cellArr">
			<view slot="icon" class="flex justify-center items-center" style="width: 30rpx;">
				<u-icon name="arrow-up" color="#60cc34" size="16"  v-if="it.type== 2"></u-icon>
				<u-icon name="arrow-down" color="#60cc34" size="16"  v-if="it.type== 1"></u-icon>
				<view class="borders" v-if="it.type== 0"></view>
			</view>
		</u-cell>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				titles: '',
				cellArr:[{
					title:'卖价',
					type:1
				},{
					title:'最高卖价',
					type:0
				},{
					title:'最低卖价',
					type:0
				},{
					title:'买价',
					type:1
				},{
					title:'最高买价',
					type:0
				},{
					title:'最低买价',
					type:0
				},{
					title:'价格修改',
					type:2
				},{
					title:'开盘价',
					type:0
				},{
					title:'收盘价',
					type:0
				},]
			};
		},
		onLoad(q) {
			this.titles = q.name
		}
	}
</script>

<style lang="scss">
	.nav {
		position: sticky;
		top: 0;
	}

	/deep/ {
		.u-navbar__content__left__text {
			font-size: 36rpx;
		}
	}

	.cell {}
	.borders{
		width: 10rpx;
		height: 10rpx;
		background: #60cc34;
		border-radius: 50%;
	}
</style>