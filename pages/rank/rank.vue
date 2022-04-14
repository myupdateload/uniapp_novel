<template>
	<view>
		<list :searchdata="searchdata"></list>
		<!-- <scroll-view  class="scroll" scroll-y="true">
			<view v-for="(item,index) in searchdata" class="views">
				<image  :src="item.image" @click="jump(index)">
				</image>
				<view class="view1">
					<view>书名：{{item.name}}</view>
					<view>作者：{{item.author}}</view>
					<view>内容：{{item.des.slice(0,25)}}...</view>
				</view>
				<view class="view2">{{index+1}}</view>
			</view>
		</scroll-view> -->
	</view>
</template>

<script>
	import list from '../../components/novel_list/novel_list.vue'
	export default {
		data() {
			return {
				searchdata:[]
			}
		},
		onLoad(){
			this.getrank()
		},
		components:{"list":list},
		methods: {
			async getrank(){
				const res = await uni.request({
					url:'http://39.96.77.250/view/bookList?&keywords=&size=100',
				})
				this.searchdata=res[1].data.result
			},
			
		}
	}
</script>

<style lang="scss">
	// .scroll{
	// 	background-color: #F5F5DC;
	// 	height: 1180rpx;
	// 	width: 100%;
	// }
	// .views{
	// 	border: 5rpx solid #FFE4C4;
	// 	background-color: #F5F5DC;
	// 	margin-bottom: 5rpx;
	// 	display: flex;
	// 	flex-direction: row;
	// 	.view1{
	// 		width: 400rpx;
	// 		display: flex;
	// 		flex-direction: column;
	// 	}
	// 	.view2{
	// 		display: flex;
	// 		flex-direction: column;
	// 		font-size: 100rpx;
	// 		color: #F0AD4E;
	// 		font-weight: 5rpx;
	// 	}
	// }
	// image{
	// 	height:250rpx ;
	// 	width: 200rpx;
	// }
</style>
