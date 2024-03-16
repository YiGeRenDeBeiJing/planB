<template>
	<view class="container">
		<view>充值金额</view>
		<u--input class="mt-4" placeholder="" border="surround" v-model="money"></u--input>
		<view class="flex flex-row mt-4">
			<u-tag text="500" type="primary" plain @click="money = '500'"></u-tag>
			<u-tag class="ml-2" text="1000" type="primary" plain @click="money = '1000'"></u-tag>
			<u-tag class="ml-2" text="2000" type="primary" plain @click="money = '2000'"></u-tag>
		</view>
		<view class="mt-4">银行卡充值</view>
		<u--input class="mt-4" placeholder="" suffixIcon="map-fill" suffixIconStyle="color: #909399" v-model="input01">
			<view slot="suffix">
				<span class="iconfont icon-fuzhi text-lg ml-4"></span>
			</view>
		</u--input>

		<u--input class="mt-4" placeholder="" suffixIcon="map-fill" suffixIconStyle="color: #909399" v-model="input02">
			<view slot="suffix">
				<span class="iconfont icon-fuzhi text-lg ml-4"></span>
			</view>
		</u--input>

		<u--input class="mt-4" placeholder="" suffixIcon="map-fill" suffixIconStyle="color: #909399" v-model="input03">
			<view slot="suffix">
				<span class="iconfont icon-fuzhi text-lg ml-4"></span>
			</view>
		</u--input>

		<view class="mt-4">付款截图</view>

		<u-upload class="mt-4" :fileList="fileList1" @afterRead="afterRead" @delete="deletePic" name="1" multiple
			:maxCount="10"></u-upload>
		
		<u-button text="提交" type="primary"></u-button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				money: '',
				input01: '',
				input02: '',
				input03: '',
				fileList1: [],
			};
		},
		methods: {
			// 删除图片
			deletePic(event) {
				this[`fileList${event.name}`].splice(event.index, 1)
			},
			// 新增图片
			async afterRead(event) {
				// 当设置 multiple 为 true 时, file 为数组格式，否则为对象格式
				let lists = [].concat(event.file)
				let fileListLen = this[`fileList${event.name}`].length
				lists.map((item) => {
					this[`fileList${event.name}`].push({
						...item,
						status: 'uploading',
						message: '上传中'
					})
				})
				for (let i = 0; i < lists.length; i++) {
					const result = await this.uploadFilePromise(lists[i].url)
					let item = this[`fileList${event.name}`][fileListLen]
					this[`fileList${event.name}`].splice(fileListLen, 1, Object.assign(item, {
						status: 'success',
						message: '',
						url: result
					}))
					fileListLen++
				}
			},
			uploadFilePromise(url) {
				return new Promise((resolve, reject) => {
					let a = uni.uploadFile({
						url: 'http://192.168.2.21:7001/upload', // 仅为示例，非真实的接口地址
						filePath: url,
						name: 'file',
						formData: {
							user: 'test'
						},
						success: (res) => {
							setTimeout(() => {
								resolve(res.data.data)
							}, 1000)
						}
					});
				})
			},
		}
	}
</script>

<style lang="scss">

</style>