<template>
	<view class="content" v-cloak>
		<view class="hid" v-if="judge">~~~~搜索不到结果~~~~</view>
		<scroll-view class="scroll"  scroll-y="true" v-if="!judge">
			<view v-for="(item,index) in searchdata" class="views">
					<image class="img1"  :src="item.image" @click="jump(index)"></image>
					<view class="view1">
						<view >书名：{{item.name}}</view>
						<view >作者：{{item.author}}</view>
						<view v-html="item.des.slice(0,38)"></view>
					</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				text:'',
				searchdata:[],
				judge:false
			}
		},
		async onLoad(value){
			let datas=JSON.parse(value.content)
			const res = await uni.request({
				url:'http://39.96.77.250/view/bookList?&keywords='+datas+'&size=100',
			})
			this.searchdata=res[1].data.result
			if(this.searchdata.length===0){
				this.judge=true
			}
			else{
				this.judge=false
			}
		},
		methods: {
			jump(index){
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
	[v-cloak]{
		display: none;
	}
	.content{
		background-color: #F5F5DC ;
		padding-bottom: 1200rpx;
	}
	.hid{
		height: 1180rpx;
		width: 100%;
		background-color: #F5F5DC;
		text-align: center;
		padding-top: 400rpx;
	}
	.views{
		border: 5rpx solid #F0AD4E;
		margin-bottom: 5rpx;
		background-color: #F5F5DC;
		display: flex;
		flex-direction: row;
		.view1{
			width: 400rpx;
			display: flex;
			flex-direction: column;
		}
	
		.img1{
			height: 300rpx;
			width: 250rpx;
			background-image: url(../../static/error.png);
		}
	}
</style>
