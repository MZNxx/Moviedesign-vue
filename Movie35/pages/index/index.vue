<template>
	<view class="page">
		 <!-- 搜索历史容器 -->
		  <view>
		  <!-- 搜索框 -->
		  <view class="search">
		  <view style="display: flex;align-items: center;">
		  <text class="iconfont icon-sousuo position-absolute text-muted"></text>
		  <input class="searchInput" v-model="inputValue" @confirm="search" placeholder="搜索" type="text" />
		  </view>
		  <view style="display: flex;flex ; flex-flow : row;" class="btstyle">
			  <button>搜索</button>
			  <button>取消</button>
		  </view>
		  
		  </view>
		  <!-- 搜索框 -->
		  
		  <!-- 搜索历史 -->
		  <view class="searchHistory">
		  <view style="display: flex;align-items: center;justify-content: space-between;box-sizing: border-box;padding: 0px 5px;">
		  <view>搜索历史:</view>
		  
		  <view style="color: red;font-size: 28px;" @click="empty">×</view>
		  </view>
		  <view class="searchHistoryItem">
		  <view v-for="(item, index) in searchHistoryList" :key="index">
		  <text>{{ item }}</text>
		  </view>
		  </view>
		  </view>
		  <!-- 搜索历史 -->
		  </view>
		     

		<!-- 搜索历史容器 -->
 
			<!-- swiper轮播图：indicator-dots说明是否显示面板指示点；autoplay是否自动切换；interval自动切换时间间隔；duration滑动动画时长	 -->
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item v-for="carousel in carouselList">
					<image :src="carousel" class="carousel"></image>
				</swiper-item>
				<!-- <swiper-item>
					-- src是图片资源路径 
					<image src="../../static/img/蝙蝠侠.jpg" class="carousel"></image>
				</swiper-item>
				<swiper-item>
					<image src="../../static/img/复仇者联盟.jpg" class="carousel"></image>
				</swiper-item>
				<swiper-item>
					<image src="../../static/img/流浪地球.jpg" class="carousel"></image>
				</swiper-item> -->
			</swiper>
			<!-- 轮播图结束 -->
			
			<!-- 热门影剧 -->
			<view class="page-block movie-hot">
				<view class="hot-title-wapper">
					<image src="../../static/img/火爆.png" class="hot-ico" ></image>
					<view class="hot-title">
						热门影剧
					</view>
				</view>
			</view>
			
			<scroll-view scroll-x="true" class="page-block hot">
			<view class="single-poster">
				<view class="post-wapper">
					<image src="../../static/img/战狼.jpg" class="poster"></image>
					<view class="movie-name">
						战狼
					</view>
					<view class="movie-score-wrapper">
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星2.png" class="star-ico"></image>
					</view>
					<view class="movie-score">9.1</view>
				</view>
			</view>
			
			<view class="single-poster">
				<view class="post-wapper">
					<image src='../../static/img/满江红.jpg' class="poster"></image>
					<view class="movie-name">
						满江红
					</view>
					<view class="movie-score-wrapper">
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星2.png" class="star-ico"></image>
					</view>
					<view class="movie-score">9.0</view>
				</view>
			</view>
			
			<view class="single-poster">
				<view class="post-wapper">
					<image src="../../static/img/无名.jpg" class="poster"></image>
					<view class="movie-name">
						无名
					</view>
					<view class="movie-score-wrapper">
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星2.png" class="star-ico"></image>
					</view>
					<view class="movie-score">8.9</view>
				</view>
			</view>
			
			<view class="single-poster">
				<view class="post-wapper">
					<image src="/static/img/速度.jpg" class="poster"></image>
					<view class="movie-name">
						速度与激情
					</view>
					<view class="movie-score-wrapper">
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星.png" class="star-ico"></image>
						<image src="/static/img/星星2.png" class="star-ico"></image>
					</view>
					<view class="movie-score">9.1</view>
				</view>
			</view>
			</scroll-view>
			
			<!-- 热门影剧 -->
			
			
			<!-- 热门预告 -->
			<view class="page-block movie-hot">
				<view class="hot-title-wapper">
					<image src="../../static/img/视频.png" class="hot-ico"></image>
					<view class="hot-title">你正在追</view>
				</view>
			</view>
			
			<scroll-view scroll-x="true" class="page-block hot">
			<view class="single-poster">
				<view class="post-wapper">
					<image src="../../static/img/战狼.jpg" class="u-like" mode="aspectFill"></image>
					<view class="movie-name">
						战狼
					</view>
				</view>
			</view>
			</scroll-view>
			<!-- 热门预告 -->

		</view>
</template>

<script>
	export default {
		data() {
			return {
				carouselList: [],
				 inputValue: '',
				 searchHistoryList: [] //搜索出来的内容
		};
	},
		onLoad() {
			// 请求轮播图数据
				uni.request({
					url:"http://localhost:8083/doc.html#/all/%E6%95%B0%E6%8D%AE%E5%BA%93/seletAllUsingGET",
					data:{
						text:'uni.request'
					},
					method:"GET",
					success: (res) => {
						if(res){
							console.log("接口调用成功");
							console.log(res.data);
							
							var carouselList = res;
							this.carouselList = carouselList;
							console.log('carouselList',carouselList);
						}
						
					}
		})
		},
	 methods: {
	// 			 search() {
	// 			 if (this.inputValue == '') {
	// 			 uni.showModal({
	// 			 title: '搜索内容不能为空'
	// 			 });
	// 			 } else {
	// 			 if (!this.searchHistoryList.includes(this.inputValue)) {
	// 			 this.searchHistoryList.unshift(this.inputValue);
	// 			 uni.setStorage({
	// 			 key: 'searchList',
	// 			 data: JSON.stringify(this.searchHistoryList)
	// 			 });
	// 			 } else {
	// 			 //有搜索记录，删除之前的旧记录，将新搜索值重新push到数组首位
	// 			 let i = this.searchHistoryList.indexOf(this.inputValue);
	// 			 this.searchHistoryList.splice(i, 1);
	// 			 this.searchHistoryList.unshift(this.inputValue);
	// 			 uni.showToast({
	// 			 title: '不能重复添加'
	// 			 });
	// 			 uni.setStorage({
	// 			 key: 'searchList',
	// 			 data: JSON.stringify(this.searchHistoryList)
	// 			 });
	// 			 }
	// 			 }
	// 			 },
	// 			 //清空历史记录
	// 			 empty() {
	// 			 uni.showToast({
	// 			 title: '已清空'
	// 			 });
	// 			 uni.removeStorage({
	// 			 key: 'searchList'
	// 			 });
				 
	// 			 this.searchHistoryList = [];
	// 			 }
	// },
	// 			 async onLoad() {
	// 			 let list = await uni.getStorage({
	// 			 key: 'searchList'
	// 			 });
				 
	// 			 console.log(list[1].data);
				 
	// 			 if (list[1].data) {
	// 			 this.searchHistoryList = JSON.parse(list[1].data);
	// 			 }
		}
	
	}
	</script>

<style>
	/* 导入index.css文件 */
	@import url("index.css");
</style>
