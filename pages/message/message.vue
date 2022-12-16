<template>
	<view>{{ title }}</view>
</template>

//刷新vue3写法
<script setup lang="ts">
import { onPullDownRefresh, onLoad } from '@dcloudio/uni-app';
import { reactive, ref } from 'vue';
const title = ref('你好');
interface dataListType {
	message: Array<string>;
}
const dataList = reactive<dataListType>({
	message: []
});
const getDataList = () => {
	uni.request({
		url: '',
		success(res: any) {
			dataList.message = res;
		}
	});
};
onLoad(() => {
	getDataList();
});
onPullDownRefresh(() => {
	getDataList();
	setTimeout(() => {
		title.value = 'This is message';
		uni.stopPullDownRefresh();
	}, 1000);
});
</script>

<style></style>
