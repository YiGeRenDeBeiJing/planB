<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="scss">	
	@import "@/uni_modules/uview-ui/index.scss";
	@import "./uni_modules/jc-tailwind/index.scss";
	@import "static/scss/main.css";

	body {
		font-family: var(--font-family);
		font-size: var(--font-size);
		-webkit-appearance: none;
		color: var(--color-text-default);
		border: 0;
	}

	.container {
		padding: 15px;
	}

	button {
		margin-bottom: 15px;
	}
</style>