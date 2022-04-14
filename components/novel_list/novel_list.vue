<template>
	<view>
		<scroll-view  class="scroll" scroll-y="true">
			<view v-for="(item,index) in searchdata" class="views">
				<image class="img1"  :src="item.image" @click="jump(index)">
				</image>
				<view class="view1">
					<view>书名：{{item.name}}</view>
					<view>作者：{{item.author}}</view>
					<view>内容：{{item.des.slice(0,25)}}...</view>
				</view>
				<view class="view2">{{index+1}}</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		props:['searchdata'],
		data() {
			return {
				
			}
		},
		methods: {
			async jump(index){
				uni.setStorageSync('id',this.searchdata[index].id)
				uni.setStorageSync('author',this.searchdata[index].author)
				uni.setStorageSync('des',this.searchdata[index].des)
				uni.setStorageSync('image',this.searchdata[index].image)
				uni.setStorageSync('latest_chapter_name',this.searchdata[index].latest_chapter_name)
				uni.setStorageSync('category',this.searchdata[index].category)
				uni.setStorageSync('name',this.searchdata[index].name)
				uni.setStorageSync('status',this.searchdata[index].status)
				uni.setStorageSync('update_time',this.searchdata[index].update_time)
				uni.navigateTo({
					url:'/pages/novel_detail/novel_detail?content='+JSON.stringify(this.searchdata[index].id)
				})
			}
		}
	}
</script>

<style lang="scss">
	.scroll{
		background-color: #F5F5DC;
		height: 100%;
		width: 100%;
	}
	.views{
		border: 5rpx solid #FFE4C4;
		background-color: #F5F5DC;
		margin-bottom: 5rpx;
		display: flex;
		flex-direction: row;
		.view1{
			width: 400rpx;
			display: flex;
			flex-direction: column;
		}
		.view2{
			display: flex;
			flex-direction: column;
			font-size: 100rpx;
			color: #F0AD4E;
			font-weight: 5rpx;
		}
	}
	.img1{
		height:300rpx ;
		width: 250rpx;
		background-image: url(../../static/error.png);
	}
</style>
