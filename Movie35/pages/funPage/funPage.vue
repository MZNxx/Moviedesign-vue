<template>
	<view>
		功能页面{{id}}
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id:""
			};
		},
		onLoad(e) {
			this.id = e.id;
		}
	}
</script>

<style lang="scss">

</style>
