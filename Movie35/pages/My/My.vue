<template>
	<view class="page page-fill">
		<!-- 我的界面头部栏 -->
		<view class="header">
			<view v-if="userIsLogin">
				<image src="../../static/logo.png" class="face"></image>
			</view>
			<view v-else>
				<image src="../../static/img/钢铁侠头像.jpg" class="face"></image>
			</view>
			
			<view v-if="userIsLogin">
				<view class="info-wapper">
					<view class="nav-info">ID:123abcsdsdsd</view>
					<view class="nav-info">钢铁侠</view>
				</view>
			</view>
			<view v-else="">
				<!-- 点击注册登陆后实现界面跳转 -->
				<navigator url="../regist/regist">
					<view class="nickname regist-login">
						注册/登陆
					</view>
				</navigator>
			</view>
			
			<view class="set-wapper" v-if="userIsLogin">
				<image src="../../static/img/设置.png" class="setting"></image>
			</view>
		</view>
	
		<!-- 功能row -->
		<view class="functionRow" v-for="item in list3" :key="id" @click="goFun(`${item.id}`)">
			<view class="functionItem">
				<view class="functionPic">
					<u-icon name="list"></u-icon> 
				</view>
			</view>
			
			<view class="functionTitle">
				{{item.functions}}
			</view>
			
			<view class="functionMore">
				<u-icon name="arrow-right"></u-icon> 
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				userIsLogin: false,
				list3:[{
						id:1,
						functions:'历史记录'
						
					},
					{
						id:2,
						functions:'我的收藏'
							
					},
					{
						id:3,
						functions:'个性主题'
								
					},
					{
						id:4,
						functions:'意见反馈'
									
					},
					]
			};
		},
		onShow() {
			var me = this;
			//用户切换
			var userInfo = uni.getStorageInfoSync("globalUser");
			if(userInfo != null && userInfo != "" && userInfo != undefined){
				me.userIsLogin = true;
				me.userInfo = userInfo;
			}else{
				me.userIsLogin = false;
				me.userInfo  = {};
			}
		},
		methods:{
			goFun(id){
				uni.navigateTo({
					url:"/pages/funPage/funPage?id="+id
				})
			}
		}
			
	}
</script>

<style lang="scss">
	@import url("me.css");
</style>
