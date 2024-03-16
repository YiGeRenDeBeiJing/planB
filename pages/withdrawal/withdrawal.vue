<template>
	<view class="container">
		<view>提现金额</view>
		<u--input class="mt-4" placeholder="" border="surround" v-model="money">
			<span slot="prefix">＄</span>
		</u--input>
		<view style="color: #888;font-size: 16rpx;" class="mt-1">可用余额：＄463.21</view>
		<u-cell  class="mt-4" :isLink="true" rightIcon="arrow-right" title="提现方式" titleStyle="font-size:20rpx" :value="types" @click="cellClick('type')"></u-cell>
		<u-cell  class="mt-1" :isLink="true" rightIcon="arrow-right" title="提现地址" titleStyle="font-size:20rpx" :value="adress" @click="cellClick('adress')"></u-cell>
		<view class="mt-4">资金密码</view>
		<u--input class="mt-4" placeholder="" v-model="input01">
		</u--input>
		<view class="mt-4">验证码</view>
		<u--input class="mt-4" placeholder="" v-model="input02">
		</u--input>
		<u-button class="mt-4" text="提交" type="primary"></u-button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				money:'',
				types:'TRC20',
				adress:'SJLDKFJDLKSJ2DFJ34DD',
				input01: '',
				input02: '',
			};
		},
		methods:{
			cellClick(it){
				if(it == 'adress'){
					let arr = ['SJLDKFJDLKSJ2DFJ34DD', 'DSDJI3SDFJ32XKD3', ]
					uni.showActionSheet({
						itemList: arr,
						success:  (res)  =>{
							console.log('选中了第' + (res.tapIndex + 1) + '个按钮');
							this.adress = arr[res.tapIndex]
						},
						fail: function (res) {
							console.log(res.errMsg);
						}
					});
				}
				if(it == 'type'){
					let arr = ['TRC20', 'TRX', ]
					uni.showActionSheet({
						itemList: arr,
						success:  (res)  =>{
							console.log('选中了第' + (res.tapIndex + 1) + '个按钮');
							this.types = arr[res.tapIndex]
						},
						fail: function (res) {
							console.log(res.errMsg);
						}
					});
				}
			}
		}
	}
</script>

<style lang="scss">

</style>