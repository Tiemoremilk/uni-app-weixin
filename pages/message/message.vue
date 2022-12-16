<template>
	<view>{{ title }}</view>
</template>

//刷新vue3写法
<script setup lang="ts">
import { onPullDownRefresh } from '@dcloudio/uni-app';
import { ref } from 'vue';
const title = ref('你好');
onPullDownRefresh(() => {
	setTimeout(() => {
		title.value = 'This is message';
		uni.stopPullDownRefresh();
	}, 1000);
});
</script>

<style></style>
