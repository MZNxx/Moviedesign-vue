<template>
	<view class="home">
		<!-- tab -->
		<view class="tab">
			<u-tabs :list="list1" @click="click"></u-tabs>
		</view>

		<!-- 显示项目 -->
		<view >

			<u-swipe-action>
				<u-swipe-action-item :options="options1" v-for="(item, index) in list2" :key="index">
					<view class="movieBox">
						<!-- 排名区 -->
						<view class="rankItem">
							<text>
								{{item.rno}}
							</text>
						</view>

						<!-- img -->
						<view class="imgItem" :style="{backgroundImage:`url(${item.rimg})`}">

						</view>

						<!-- 放各种文字的地方 -->
						<view class="textBox">
							<!-- title -->
							<view class="title">
								<text>
									{{item.rtitle}}
								</text>
							</view>

							<view class="content">
								<text>
									{{item.rcontent}}
								</text>
							</view>

						</view>
					</view>

				</u-swipe-action-item>
			</u-swipe-action>



			<!-- 收藏按钮 -->
			<!-- <view class="textMore">
				<u-icon name="more-dot-fill" @click="showSheet"></u-icon>
			</view> -->
		</view>

		<!-- 显示sheet -->
		<!-- 		<view class="sheet">
			<u-action-sheet :list="sheetList" v-model="show"></u-action-sheet>
		</view> -->
	</view>

</template>

<script>
	export default {
		data() {
			return {
				// 	show: false,
				// 	sheetList: [{
				// 		text: '点赞',
				// 		color: 'blue',
				// 		fontSize: 28
				// 	}, {
				// 		text: '分享'
				// 	}, {
				// 		text: '评论'
				// 	}
				// ],
				options1: [{
					text: '收藏',
					style: {
						backgroundColor: '#3c9cff'
					}
				}, {
					text: '删除'
				}],
				img: "https://img0.baidu.com/it/u=3262881422,578376304&fm=253&fmt=auto&app=120&f=JPEG?w=1280&h=800",
				list1: [{
						name: '推荐',
					}, {
						name: '电影'
					},
					{
						name: '悬疑'
					}, {
						name: '科幻'
					}, {
						name: '爱情'
					}, {
						name: '喜剧'
					}, {
						name: '教育'
					}
				],
				list2: [
					//{
					// 	id: 1,
					// 	no: 'NO:1',
					// 	img: 'https://img0.baidu.com/it/u=3262881422,578376304&fm=253&fmt=auto&app=120&f=JPEG?w=1280&h=800',
					// 	rtitle:'流浪地球',
					// 	rcontent:'《流浪地球》是由吴京、吴孟达等领衔主演的科幻冒险电影。',
					// }
				]
			}
		},
		onReady() {
			this.getData();
		},

		methods: {

			click(item) {
				console.log('item', item);
			},
			getData() {
				uni.request({
					url: "http://localhost:8083/getimgurl/getrecommend",
					method: "GET",
					success: (res) => {
						if (res) {
							console.log(JSON.stringify(res));
							this.list2 = res.data;
							console.log("list2", this.list2);
						} else {
							console.log("获取失败");
						}
					},
				})
			}


		}
	}
</script>

<style lang="scss">
	view {
		box-sizing: border-box;
	}
	page{
		background-color: #f8f8f8;
	}
	.tab{
		background-color: #fff;
	}
	.movieBox {
		background: #fff;
		display: flex;
		align-items: top;
		justify-content: space-evenly;
		padding:12rpx;
		border: 1rpx solid #55aaff;
		border-radius: 16rpx;
		position: relative;
		margin: 4rpx 12rpx;
		.rankItem {
			width: 10%;
			padding-top: 50rpx;
		}

		.imgItem {
			width: 20%;
			height: 150rpx;
			background-size: 100% 100%;
			background-repeat: no-repeat;
		}

		.textBox {
			width: 50%;
			display: flex;
			flex-direction: column;

			.title {
				// padding-bottom: 18rpx;

				overflow: hidden;
				-webkit-line-clamp: 2;
				text-overflow: ellipsis;
				display: -webkit-box;
				-webkit-box-orient: vertical;


				font-size: 45upx;
				font-weight: bold;
			}
		}

		.textMore {
			height: 28rpx;
			width: 28rpx;
			position: absolute;
			right: 24rpx;
			top: 24rpx;
		}
	}
</style>
