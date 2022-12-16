## 探索uni-app使用笔记

个人使用uni-app中遇到一些困惑及解决，可能稍有不对或有笨拙，大佬请勿耻笑，持续更新中

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
