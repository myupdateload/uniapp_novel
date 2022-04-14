<template>
	<scroll-view  class="scroll" scroll-y="true">
		<view class="views">目录</view>
		<view  v-for="(item,index) in chapterdata" class="views" @click="jump(index)">
				<view>{{item.name}}{{item.chaperIdx}}</view>
		</view>
	</scroll-view>
</template>

<script>
	export default {
		data() {
			return {
				date:'',
				chapterdata:[]
			}
		},
		onLoad(id){
			const datas=JSON.parse(id.content)
			this.date=datas
			this.getchapter()
		},
		methods: {
			async getchapter(){
				const res = await uni.request({
					url:'http://39.96.77.250/view/chapters?&bookId='+this.date,
				})
				this.chapterdata=res[1].data.result
			},
			jump(index){
				const tranform = [this.chapterdata[index].book,index]
				uni.navigateTo({
					url:'/pages/read/read?content='+JSON.stringify(tranform)
				})
			}
		}
	}
</script>

<style lang="scss">
	image{
		height: 300rpx;
		width: 250rpx;
	}
	.scroll{
		background-color: #F5F5DC;
		height: 100%;
		width: 100%;
		padding-bottom: 1180rpx;
	}
	.views{
		border-bottom: 3rpx solid  #007AFF;
		margin-left: 15rpx;
		margin-right: 15rpx;
	}
</style>
