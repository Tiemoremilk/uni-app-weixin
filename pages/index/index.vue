<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{ title }}</text>
		</view>
	</view>
</template>

<script>
//刷新vue2写法
export default {
	data() {
		return {
			title: 'Hello, This is index'
		};
	},
	onLoad(options) {
		console.log('页面加载了');
	},
	onPullDownRefresh() {
		console.log('下拉刷新>>>>');
		this.title = '欢迎使用';
		setTimeout(() => {
			uni.stopPullDownRefresh();
		}, 1000);
	},
	onReachBottom: () => {},
	methods: {}
};
</script>

<style>
.content {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}

.logo {
	height: 200rpx;
	width: 200rpx;
	margin-top: 200rpx;
	margin-left: auto;
	margin-right: auto;
	margin-bottom: 50rpx;
}

.text-area {
	display: flex;
	justify-content: center;
}

.title {
	font-size: 36rpx;
	color: #8f8f94;
}
</style>
