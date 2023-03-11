<template>
	<view class="body">
		<form @submit="formsubmit">
		<view class="face-wapper">
			<image src="../../static/img/蜘蛛侠.jpg" class="face"></image>
		</view>
		
		<view class="info-wapper">
			<label class="words-lbl">账号</label>
			<input name="username" type="text" value="" class="input" placeholder="请输入账号" placeholder-class="graywords"/>
		</view>
		
		<view class="info-wapper" style="margin-top: 40upx;">
			<label class="words-lbl">密码</label>
			<input name="password" type="text" value="" password="true" class="input" placeholder="请输入密码" placeholder-class="graywords"/>
		</view>
		
		<button type="primary" form-type="submit" style="margin-top: 60upx;width: 90%;">注册/登陆</button>
		</form>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		methods:{
			// 获取输入的账号密码
			formsubmit(e){
				var me = this;
				var username = e.detail.value.username;
				var password = e.detail.value.password;
				// 发起注册/登陆的请求(需要后端接口)
				var serverUrl = me.serverUrl;
				uni.request({
					url:serverUrl + 'http://localhost:8083/doc.html#/all/user-controller/loginUserUsingPOST',
					data:{
						"username": username,
						"password": password
					},
					method:"POST",
					success: (res) => {
						// 获取数据库真实数据,并判断状态是否为200
						if(res.data.status == 200){
							var userInfo = res.data.data;
							// 保存用户信息到全局的缓存中
							uni.setStorageSync("globalUser",userInfo);
							// 切换页面跳转,使用tab切换api
							uni.switchTab({
								url: "../My/My"
							})
						}
						
					}
				})
			}
		}
	}
</script>

<style lang="scss">
  @import url("regist.css");
</style>
