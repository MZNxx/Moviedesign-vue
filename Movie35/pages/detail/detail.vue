<template>
	<view>
		文章详情
		<view class="test">
			{{mid}}
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mid:""
			};
		},
		onLoad(e) {
			console.log(e);
			this.mid = e.mid;
		}
	}
</script>

<style lang="scss">

</style>
