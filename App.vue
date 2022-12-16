<script>
export default {
	onLaunch: function() {
		console.log('App Launch');
	},
	onShow: function() {
		console.log('App Show');
	},
	onHide: function() {
		console.log('App Hide');
	},
	onError(err) {
		console.log('错误' + err);
	}
};
</script>

<style>
/*每个页面公共css */
</style>
