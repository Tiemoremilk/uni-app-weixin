## 探索uni-app使用笔记

个人使用uni-app中遇到一些困惑及解决，可能稍有不对或有笨拙，持续更新中

### 前置知识

- uni-app生态及其介绍：https://ke.qq.com/course/3169971#term_id=103296764

- uni-app指南：https://uniapp.dcloud.net.cn/
### 使用小记

- [x] **生命周期相关操作**

```typescript
//刷新vue3写法
<script setup lang="ts">
import { onPullDownRefresh } from '@dcloudio/uni-app';
import {  ref } from 'vue';
const title = ref('Hello,Word');
onPullDownRefresh(() => {
	setTimeout(() => {
		title.value = '你好，世界';
		uni.stopPullDownRefresh();
	}, 1000);
});
</script>
```

```javascript
//刷新vue2写法
<script>
export default {
	data() {
		return {
			title: 'Hello, This is uni-app'
		};
	},
	onPullDownRefresh() {
		this.title = '你好';
		setTimeout(() => {
			uni.stopPullDownRefresh();
		}, 1000);
	},
	methods: {}
};
</script>
```

比较使用而言最大的区别就是 setup语法糖使用onPullDownRefresh需要自己从@dcloudio/uni-app引入，其实onReachBottom这些也是同样的用法，详细可以看官网的用法
https://uniapp.dcloud.net.cn/tutorial/page.html 
我们需要注意的是在vue里 setup是在created生命周期函数被完全初始化之前执行的函数 ， 使用组合式API没有 beforeCreate 和 created 这两个生命周期 ，那么在uni-app组件生命周期里应该也是一样的



- [x] **谈谈从vsCode过渡到Hbuildx**

为什么搭建uni-app，建议使用Hbuildx ?
首先我们要明白的是vsCode只是一个代码编辑管理的工具，在uni-app中我们做跨端需要有不同的环境，而Hbuildx刚好满足我们的需求，另外他内置了很多开发模块，纵然vsCode通过插件依赖能做到，但在开发uni-app建议还是使用Hbuildx，因为它更方便快捷 https://www.dcloud.io/hbuilderx.html

```typescript
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
```

个人使用发现一个问题，在vsCode中有些情况返回数据不定义类型不会提示，但在Hbuildx会爆红（例如上例代码success（）中res的any类型），有可能是插件问题，vsCode可以自己找到，Hbuildx装了插件也不太行。但这无疑会让代码规范很多，让过度依赖插件的人修正过来，虽然刚开始很难受