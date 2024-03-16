<template>
	<view class="container">
		<view class="nav">
			<u-navbar title="" autoBack @rightClick="rightClick" placeholder>
			</u-navbar>
		</view>

		<view class="text-2xl">您好，</view>
		<view class="text-2xl">欢迎您！</view>
		<view class="mt-4 text-center text-lg">用户注册</view>

		<u--input class="mt-4" placeholder="请输入手机号码" border="surround" v-model="phone"
			placeholderStyle="font-size:16rpx">
			<view class="flex flex-row items-center" slot="prefix" style="padding:0 10rpx 0 0;" @click="countryClick">
				<image style="width: 40rpx;height: 40rpx;" :src="country.image" mode="aspectFit"></image>
				<span>+{{country.txt}}</span>
				<u-icon class="ml-2" name="arrow-down" color="#888" size="10"></u-icon>
			</view>
		</u--input>

		<u--input class="mt-4" placeholder="密码必须由 (6~16) 位字母" border="surround" v-model="password"
			placeholderStyle="font-size:16rpx">
		</u--input>
		<u--input class="mt-4" placeholder="请输入验证码" border="surround" v-model="password"
			placeholderStyle="font-size:16rpx">
			<view slot="suffix">
				<u-button type="primary" size="mini" @tap="getCode">{{tips}}</u-button>
			</view>
		</u--input>
		<u-button class="mt-16" text="注册" type="primary"></u-button>
		<u-code :seconds="seconds" @end="end" @start="start" ref="uCode" @change="codeChange"></u-code>
		<u-picker :show="showcountry" :columns="columns" @confirm="countryConfirm"></u-picker>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				phone: '',
				password: '',
				country: {
					image: '/static/zIZfYr.png',
					txt: '86'
				},
				showcountry: false,
				columns: [
					['86', '52']
				],
				tips: '',
				// refCode: null,
				seconds: 10,
			};
		},
		methods: {
			countryClick() {
				this.showcountry = true
			},
			countryConfirm(val) {
				let imgs = ['/static/zIZfYr.png', '/static/ie6rMj.png']
				this.country.txt = val.value[0]
				this.country.image = imgs[val.indexs[0]]
				this.showcountry = false
			},
			codeChange(text) {
				this.tips = text;
			},
			getCode() {
				if (this.$refs.uCode.canGetCode) {
					// 模拟向后端请求验证码
					uni.showLoading({
						title: '正在获取验证码'
					})
					setTimeout(() => {
						uni.hideLoading();
						// 这里此提示会被this.start()方法中的提示覆盖
						uni.$u.toast('验证码已发送');
						// 通知验证码组件内部开始倒计时
						this.$refs.uCode.start();
					}, 2000);
				} else {
					uni.$u.toast('倒计时结束后再发送');
				}
			},
			end() {
				uni.$u.toast('倒计时结束');
			},
			start() {
				uni.$u.toast('倒计时开始');
			}
		}
	}
</script>

<style lang="scss" scoped>
/deep/ {
	.u-input{
		padding: 26rpx 18rpx !important;
		position: relative;
		.u-button{
			position: absolute;
			top: 0;
			right: 0;
			width: 30%;
			height: 100rpx;
		}
	}
}
</style>