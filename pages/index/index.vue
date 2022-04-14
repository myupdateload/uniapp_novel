<template>
	<view class="content">
		<view class="search">
			<input placeholder="请输入查找的小说" v-model="keyword"  />
			<button class="btn" type="primary" @click="btn">搜索</button>
		</view>
		<view>
			<ul class="ul" v-for="(item,index) in searchdata.slice(0,6)">
				<li class="li" @click="jump(item.name)">{{item.name}}</li>
			</ul>
		</view>
		<view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				keyword:'',
				size:100,
				searchdata:[],
				text:'',
				shoucangkey:["2960","4429"]
			}
		},
		onLoad(){
			uni.setStorageSync("shoucangkeyid",JSON.stringify(this.shoucangkey))
		},
		methods: {
			async jump(name){
					uni.navigateTo({
						url:'/pages/search/search?content='+JSON.stringify(name)
					})
				},
			async btn(){
				uni.navigateTo({
					url:'/pages/search/search?content='+JSON.stringify(this.keyword)
				})
			}
		},
		watch:{
			keyword:{
				handler(newValue,oldValue){
					if(newValue===''){
						this.searchdata=[]
					}else{
						let time=100;
						setTimeout(async()=>{
							const res = await uni.request({
								url:'http://39.96.77.250/view/bookList?&keywords='+newValue+'&size=100'
							})
							this.searchdata=res[1].data.result
						},time)
					}
				}
			}
		}
		
		
	}
</script>

<style lang="scss">
	.ul{
		margin-left: -140rpx;
		border-right: 5rpx solid #F5F5DC;
		border-left: 5rpx solid #F5F5DC;
		border-bottom: 5rpx solid #F5F5DC;
		border-radius: 10rpx;
		width: 400rpx;
		list-style: none;
		.li{
			
			height: 80rpx;
			// border-top: 5rpx solid #F5F5DC;
			border-radius: 10rpx;
			letter-spacing: 5rpx;
		}
	}
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		margin-top: 200rpx;
		width: 100%;
		.search{
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			input{
				margin-left: 20rpx;
				border-radius: 10rpx;
				border: #007AFF solid;
				height: 100rpx;
				width: 500rpx;
			}
			.btn{
				height: 110rpx;
				width: 150rpx;
				margin-left: 10rpx;
				background-color: #007AFF;
			}
		}
	}
</style>
