<template>
	<view class="content">
		<image :src="image" class="img1"></image>
		<view class="viewss">书名：{{name}}</view>
		<view class="viewss">作者：{{author}}</view>
		<view class="viewss">分类：{{category}} &nbsp 状态：{{status}}</view>
		<view class="viewss">最后章节名称：{{latest_chapter_name}}</view>
		<view class="viewss">最后更新时间：{{update_time}}</view>
		<view >
			<!-- <view><button class="btn" ref="shoucangbtn" @click="shoucang">{{shoucangmessage}}</button></view> -->
			<button class="btn" @click="read">开始阅读</button>
		</view>
		<text>详情介绍：</text></text><view class="deal"  v-html="des"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id:0,
				author:'',
				des:'',
				image:'',
				latest_chapter_name:'',
				category:'',
				name:'',
				status:'',
				update_time:'',
				is_shoucang:false,
				shoucangmessage:'未收藏'
			}
		},
		onLoad(){
			this.id=uni.getStorageSync('id'),
			this.author=uni.getStorageSync('author'),
			this.des=uni.getStorageSync('des'),
			this.image=uni.getStorageSync('image'),
			this.latest_chapter_name=uni.getStorageSync('latest_chapter_name'),
			this.category=uni.getStorageSync('category'),
			this.name=uni.getStorageSync('name'),
			this.status=uni.getStorageSync('status'),
			this.update_time=uni.getStorageSync('update_time')
			uni.removeStorageSync('id'),
			uni.removeStorageSync('author'),
			uni.removeStorageSync('des'),
			uni.removeStorageSync('image'),
			uni.removeStorageSync('latest_chapter_name'),
			uni.removeStorageSync('category'),
			uni.removeStorageSync('name'),
			uni.removeStorageSync('status'),
			uni.removeStorageSync('update_time'),
			this.panding()
		},
		methods: {
			panding(){
				let shoucangkey=uni.getStorageSync("shoucangkeyid")
				shoucangkey=shoucangkey.replace(/"/g,'')
				shoucangkey=shoucangkey.replace('[','')
				shoucangkey=shoucangkey.replace(']','')
				shoucangkey=shoucangkey.split(",")
				let strid=(this.id).toString()
				let num=shoucangkey.indexOf(strid)
				if(num===-1){
					// this.$refs.shoucangbtn.backgroundColor=#DEB887,
					this.shoucangmessage='未收藏',
					this.is_shoucang=false
				}else{
					// this.$refs.shoucangbtn.backgroundColor=#FFF,
					this.shoucangmessage='已收藏',
					this.is_shoucang=true
				}
			},
			shoucang(){
				if(this.is_shoucang===false){
					let shoucangkey=uni.getStorageSync("shoucangkeyid")
					// shoucangkey=shoucangkey.toString()
					shoucangkey=shoucangkey.replace(/"/g,'')
					shoucangkey=shoucangkey.replace('[','')
					shoucangkey=shoucangkey.replace(']','')
					shoucangkey=shoucangkey.split(",")
					let strid=(this.id).toString()
					shoucangkey.push(strid)
					uni.setStorageSync('shoucangkeyid',JSON.stringify(shoucangkey))
					// this.$refs.shoucangbtn.backgroundColor=#FFF,
					this.shoucangmessage='已收藏'
				}
				// else{
				// 	let shoucangkey=uni.getStorageSync("shoucangkeyid")
				// 	// shoucangkey=shoucangkey.toString()
				// 	shoucangkey=shoucangkey.replace(/"/g,'')
				// 	shoucangkey=shoucangkey.replace('[','')
				// 	shoucangkey=shoucangkey.replace(']','')
				// 	shoucangkey=shoucangkey.split(",")
				// 	let strid=(this.id).toString()
				// 	let num=shoucangkey.indexOf(strid)
				// 	shoucangkey.splice(num,1)
				// 	uni.setStorageSync('shoucangkeyid',JSON.stringify(shoucangkey))
				// 	// this.$refs.shoucangbtn.backgroundColor=#DEB887,
				// 	this.shoucangmessage='未收藏'
				// }
				
			},
			getchapter(){
				
			},
			read(){
				uni.navigateTo({
					url:'/pages/novel_info/novel_info?content='+JSON.stringify(this.id)
				})
			}
		}
	}
</script>

<style lang="scss">

	.content{
		height: 100%;
		width: 100%;
		background-color:#F5F5DC ;
		.btn{
			height: 100rpx;
			width: 350rpx;
			background-color: #DEB887;
			
		}
		.deal{
			padding-bottom: 400rpx;
			margin-left: 15rpx;
			margin-right: 15rpx;
		}
		.img1{
			height: 600rpx;
			width: 100%;
			background-image: url(../../static/error.png);
		}
		.viewss{
			margin-left: 15rpx;
			margin-right: 15rpx;
		}
	}
</style>
