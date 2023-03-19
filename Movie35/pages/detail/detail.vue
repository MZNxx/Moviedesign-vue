<template>
	<view class="home">
		<!-- 文章头部 -->
		<view class="titleBox">
			<view class="title">
				
			</view>
			
			<view class="author">
				{{dataList.author}}
			</view>
					
		</view>
		
		<!-- 文章图片 -->
		<view class="textImage">
			<image >
				
			</image>
		</view>
		
		<!-- 文章内容 -->
		<view class="textContent">
			住高档酒店江景房 被人看光光
			
			听友徐先生投诉，通过易龙APP预订了杭州康莱德酒店一晚1649元的江景房。3月6日和女友一起入住。第二天一早，小情侣俩人拉开窗帘看江景，发现窗外居然有人！而此时，两人都没有穿衣服！
			
			徐先生：我们入住的是41层。拉开窗帘的时候，突然看到房间外面有人在擦玻璃！我和我女朋友都没穿衣服，隐私被他侵犯了！我们都有心理阴影了！房间里面放了一个温馨提示，写的是“近期有搞玻璃卫生，在必要时候要把窗户关起来”。
			
			在入住的时候酒店没有提醒，到底是哪段时间不能打开窗帘？我们本来当天要退的，酒店说等他们消息再住两天。结果这两天时间，他们所谓的高层都没出现，又叫我们付房租，又多掏两天这么贵的冤枉钱。 我的诉求：第一书面道歉，杜绝后续给其他客户造成不良影响；第二要求退掉住店费用，赔偿精神损失。
			
			杭州康莱德酒店公关部钟女士回复：对这样的事情表示抱歉。清洗玻璃外墙的公司由物业公司统一安排。受来福士楼层高度、天气等因素影响，清洗时间会有调整。没有办法确定清洗时间。加之每一个客人作息时间不一样，很难电话或按门铃通知客人。顶多只能在房间里放置温馨提示。
			
			我们已经跟相关部门在沟通，今后在清洗玻璃期间，在前台放置一个温馨提示小立牌。在客人办理入住的时候告知客人，或在房卡里塞一个温馨提示小纸条，和房卡一起给到客人。
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				aid:"",
				dataList:[]
			};
		},
		onLoad(e) {
			console.log(e);
			this.aid = e.aid;
			this.getTextData(this.aid);
		},
		methods:{
			getTextData(aid){
				let newId = parseInt(aid)
				console.log("newIdtype",typeof(newId));
				console.log("newId",newId);
				uni.request({
					url:'http://localhost:8083/article/click?'+this.newId,
					data:{
						id:newId
					},
					method:"GET",
					success:(res=>{
						this.data = res;
						console.log("res",res);
					})
				})
			}
		}
	}
</script>

<style lang="scss">
	view{
		box-sizing: border-box;
	}
	.titleBox{
		// display: flex;
		padding: 12rpx;
		margin: 12rpx;
		// border-radius: 16rpx;
		.title{
			font-size: 42rpx;
			font-weight: bold;
			word-wrap:break-word;
		}
		.author{
			padding-top: 20rpx;
			font-size: 28rpx;
			color: #888;
		}
	}
	.textImage{
		padding: 12rpx;
		width: 98%;
	}
	.textContent{
		font-size: 32rpx;
		padding: 24rpx;
		word-wrap:break-word;
	}
</style>
