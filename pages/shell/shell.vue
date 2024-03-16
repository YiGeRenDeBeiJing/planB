<template>
	<view>
		<view class="container">
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
						<span class="iconfont icon-money text-2xl"></span>
					</view>
				</u-navbar>
			</view>
			<view class="mt-2 cellB text-center">
				即时执行
			</view>
			<view class="mt-4 cellA text-center flex justify-between items-center">
				<view class="gray">-0.5</view>
				<view class="gray">-0.1</view>
				<view class="gray">-0.01</view>
				<view class="font-bold">0.01</view>
				<view class="blue">+0.01</view>
				<view class="blue">+0.1</view>
				<view class="blue">+0.5</view>
			</view>
			<view class="flex justify-center item-center cellC mt-4 font-bold">
				<view class="flex flex-row items-end text-lg red">
					1.0853 <span class="text-2xl font-bold" style="line-height: 48rpx;">84²</span>
				</view>
				<view class="flex flex-row items-end text-lg blue  ml-4">
					1.0853 <span class="text-2xl font-bold" style="line-height: 48rpx;">84²</span>
				</view>
			</view>
			<view class="flex justify-center item-center cellbc mt-4">
				<view class="cellA flex justify-between items-center add">
					<u-icon name="minus" color="#2979ff" size="10"></u-icon>
					SL
					<u-icon name="plus" color="#2979ff" size="10"></u-icon>
				</view>
				<view class="cellC ml-8 flex justify-between items-center add">
					<u-icon name="minus" color="#2979ff" size="10"></u-icon>
					TP
					<u-icon name="plus" color="#2979ff" size="10"></u-icon>
				</view>
			</view>
			<view class="cellA mt-4 flex justify-between items-center add">
				<u-icon name="minus" color="#2979ff" size="10"></u-icon>
				<view class="flex justify-center items-center" style="width: 50%;color: #888;font-size: 30rpx;">
					偏差
					<span class="ml-4" style="font-weight: bold;color: #333;">3</span>
				</view>
				<u-icon name="plus" color="#2979ff" size="10"></u-icon>
			</view>
			<echarts class="mt-4" ref="charts" :option="option" style="height: 260px;"></echarts>
		</view>
		
		<view class="flex justify-between items-center btns">
			<view class="red">SELL</view>
			<view class="blue" style="border-left: 3px solid #fff;">BUY</view>
		</view>
	</view>
</template>

<script>
	import echarts from '@/components/echarts.vue';
	export default {
		components: {
			echarts
		},
		data() {
			return {
				option: {}
			};
		},
		onReady() {
			uni.request({
				url: 'https://echarts.apache.org/examples/data/asset/data/life-expectancy-table.json',
				success: (val) => {
					this.runs(val.data)
				}
			})
		},
		methods: {
			runs(_rawData) {
				// console.log(JSON.stringify(_rawData));
				// var countries = ['Australia', 'Canada', 'China', 'Cuba', 'Finland', 'France', 'Germany', 'Iceland', 'India', 'Japan', 'North Korea', 'South Korea', 'New Zealand', 'Norway', 'Poland', 'Russia', 'Turkey', 'United Kingdom', 'United States'];]
				const countries = [
					'Finland',
					'France',
				];
				_rawData.forEach((it, index) => {
					if (index != 0) {
						it[0] = 1.08485
						var randomNumber = index < 1000 ? (0.00001 + Math.random() * (0.0001 - 0.00001)) : (
							0.0001 + Math.random() * (0.0008 - 0.0003));
						it[0] += randomNumber
						// it[0] = Number(it[0]).toFixed(5)
						console.log(typeof it[0])
					}
					
				})
				const datasetWithFilters = [];
				const seriesList = [];
				countries.forEach((country) => {
					var datasetId = 'dataset_' + country;
					datasetWithFilters.push({
						id: datasetId,
						fromDatasetId: 'dataset_raw',
						transform: {
							type: 'filter',
							config: {
								and: [{
										dimension: 'Year',
										gte: 1950
									},
									{
										dimension: 'Country',
										'=': country
									}
								]
							}
						}
					});
					seriesList.push({
						type: 'line',
						datasetId: datasetId,
						showSymbol: false,
						name: country,
						endLabel: {
							show: true,
							formatter: function(params) {
								//params.value[3] + ': ' +
								return  params.value[0].toFixed(5);
							},
							color:country != 'Finland'? 'green':'blue'
						},
						labelLayout: {
							moveOverlap: 'shiftY'
						},
						emphasis: {
							focus: 'series'
						},
						encode: {
							x: 'Year',
							y: 'Income',
							label: ['Country', 'Income'],
							itemName: 'Year',
							tooltip: ['Income']
						}
					});
				});
				let option = {
					animationDuration: 8000,
					dataset: [{
							id: 'dataset_raw',
							source: _rawData
						},
						...datasetWithFilters
					],
					tooltip: {
						order: 'valueDesc',
						trigger: 'axis'
					},
					xAxis: {
						show: false,
						type: 'category',
						nameLocation: 'middle'
					},
					yAxis: {
						name: '',
						type: 'value',
						position: 'right', // 将 Y 轴放在右边
						min: 1.08485, // 设置 Y 轴的最小值
						max: 1.08555, // 设置 Y 轴的最大值
						axisLabel: {
							formatter: function(value, index) {
								console.log(value)
								// 将轴上的值格式化为需要的精度
								return value.toFixed(5); // 将数值保留到小数点后5位
							}
						},
						interval: 0.0001
					},
					grid: {
						right: 60,
						left: 0,
						top:10,
						bottom:10
					},
					series: seriesList
				};
				this.option = option
			}
		}
	}
</script>

<style lang="scss" scoped>
	.cellB {
		border-bottom: 1px solid #999;
		padding: 24rpx 0;
		position: relative;

		&:after {
			content: ' ';
			position: absolute;
			bottom: 0;
			left: 0;
			height: 10rpx;
			width: 2rpx;
			background: #999;
		}

		&:before {
			content: ' ';
			position: absolute;
			bottom: 0;
			right: 0;
			border-width: 0 20rpx 20rpx 0;
			border-style: solid;
			border-color: transparent transparent #999 transparent;
			transform: rotate(266deg);
		}
	}

	.cellA {
		border-bottom: 1px solid #999;
		padding: 24rpx 0;
		position: relative;
		font-size: 32rpx;

		&:after {
			content: ' ';
			position: absolute;
			bottom: 0;
			left: 0;
			height: 10rpx;
			width: 2rpx;
			background: #999;
		}

		&:before {
			content: ' ';
			position: absolute;
			bottom: 0;
			right: 0;
			height: 10rpx;
			width: 2rpx;
			background: #999;
		}

		view {
			width: 14.28%;
			text-align: center;
		}

		.gray {
			color: #a2a2a2;
		}

		.blue {
			color: #64859f;
		}
	}

	.cellC {
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

	}

	.cellbc {
		.cellA {
			width: 40%;
			border-bottom: 1px solid green;

			&:after {
				background: green;
			}

			&:before {
				background: green;
			}
		}

		.cellC {
			width: 40%;
			border-bottom: 1px solid orange;
			position: relative;

			&:after {
				content: ' ';
				position: absolute;
				bottom: 0;
				left: 0;
				height: 10rpx;
				width: 2rpx;
				background: orange;
			}

			&:before {
				content: ' ';
				position: absolute;
				bottom: 0;
				right: 0;
				height: 10rpx;
				width: 2rpx;
				background: orange;
			}
		}

		.add {
			position: relative;
		}
	}
	.btns{
		width: 100%;
		height: 80rpx;
		background: #f7f7f7;
		font-weight: bold;
		view{
			width: 50%;
			display: flex;
			justify-content: center;
			align-items: center;
			height: 80rpx;
		}
		.red{
			color: #a42f2a;
		}
		.blue{
			color: #2366c2;
		}
	}
	/deep/ {
		.u-icon {
			display: flex;
			justify-content: center;
			align-items: center;

			span {
				font-weight: bold;
			}
		}
	}
</style>