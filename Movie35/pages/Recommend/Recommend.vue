<template>
	<view class="home">
		<!-- tab -->
		<view class="tab">
			<u-tabs :list="list1" @click="click"></u-tabs>
		</view>
		
		<!-- 显示项目 -->
		<view class="movieBox" v-for="item in list2" :key="list2.id">
	
			<!-- 排名区 -->
			<view class="rankItem">
				<text>
					{{item.no}}
				</text>
			</view>
			
			<!-- img -->
			<view class="imgItem" 
			:style="{backgroundImage:`url(${item.img})`}">
				
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
		
	</view>
	
</template>

<script>

	export default {
		data() {
			return {
				img:"https://img0.baidu.com/it/u=3262881422,578376304&fm=253&fmt=auto&app=120&f=JPEG?w=1280&h=800",
				 list1: [ {
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
				                }],
			list2: [{
				id: 1,
				no: 'NO:1',
				img: 'https://img0.baidu.com/it/u=3262881422,578376304&fm=253&fmt=auto&app=120&f=JPEG?w=1280&h=800',
				rtitle:'流浪地球',
				rcontent:'《流浪地球》是由吴京、吴孟达等领衔主演的科幻冒险电影。',
			}
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
							getData(){
								uni.request({
									url:"http://localhost:8083/doc.html#/all/%E6%8E%A8%E8%8D%90%E9%A1%B5/getrecommendUsingGET",
									method:"GET",
									success: (res) => {
										if(res){
											console.log("res",res);
										}
									        
									    },
								})
							}
						
		        
		      }
	}
</script>

<style lang="scss">
	view{
		box-sizing: border-box;
	}
	.movieBox{
		display: flex;
		align-items: top;
		justify-content: space-evenly;
		
		.rankItem{
			width: 10%;
			padding-top: 50rpx;
		}
		.imgItem{
			width: 20%;
			height: 150rpx;
			background-size: 100% 100%;
			background-repeat: no-repeat;
		}
		.textBox{
			width: 50%;
			display: flex;
			flex-direction: column;
			
			.title{
				// padding-bottom: 18rpx;
				
				font-size: 45upx;
				font-weight: bold;
			}
		}
	}
	
</style>