<template>
	<view class="one">
		<view class="btn">
			<button  @click="btn1">玄幻</button>
			<button  @click="btn2">修真</button>
			<button  @click="btn3">都市</button>
			<button  @click="btn4">穿越</button>
			<button  @click="btn5">网游</button>
			<button  @click="btn6">科幻</button>
			<button  @click="btn7">完本</button>
			<button  @click="btn8">其他</button>
		</view>
		<view class="two" >
			<scroll-view class="scroll"  scroll-y="true">
				<view v-for="(item,index) in searchdata" class="views">
						<image class="img1"  :src="item.image"   @click="jump(index)"></image>
						<view class="view1">
							<view >书名：{{item.name}}</view>
							<view >作者：{{item.author}}</view>
							<view >内容：{{item.des.slice(0,35)}}...</view>
						</view>
				</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				number:1,
				searchdata:[],
				shu:1,
			}
		},
		onLoad(){
			this.getlist()
		},
		onReachBottom(){
			this.shu++
			this.getlist()
		},
		methods: {
			btn1(){
				this.number = 1,
				this.searchdata=[],
				this.getlist()
			},
			btn2(){
				this.number = 2,
				this.searchdata=[],
				this.getlist()
			},
			btn3(){
				this.number = 3,
				this.searchdata=[],
				this.getlist()
			},
			btn4(){
				this.number = 4,
				this.searchdata=[],
				this.getlist()
			},
			btn5(){
				this.number = 5,
				this.searchdata=[],
				this.getlist()
			},
			btn6(){
				this.number = 6,
				this.searchdata=[],
				this.getlist()
			},
			btn7(){
				this.number = 7,
				this.searchdata=[],
				this.getlist()
			},
			btn8(){
				this.number = 8,
				this.searchdata=[],
				this.getlist()
			},
			async getlist(){
				const res = await uni.request({
					url:'http://39.96.77.250/view/bookList?&category='+this.number+'&page='+this.shu,
				})
				this.searchdata = [...this.searchdata,...res[1].data.result]
			},
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
	.btn{
		display: flex;
		flex-direction: row;
		background-color: #F5F5DC ;
		button{
			height: 200rpx;
			width: 150rpx;
			background-color:#F0AD4E ;
			margin-left: 5rpx;
			text-align: center;
		}
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
