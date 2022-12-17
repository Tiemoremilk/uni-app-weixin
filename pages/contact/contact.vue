<template>
	<view>
		<view><button size="mini" type="default" @click="chooseImg">上传图片</button></view>
	</view>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
// const imgArr: Array<string> = ref();
const imgArr = ref<Array<string>>([]);
const chooseImg = () => {
	uni.chooseImage({
		count: 5,
		success(res: any) {
			imgArr.value = res.tempFilePaths;
		}
	});
};
</script>

<style></style>
