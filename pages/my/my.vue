<template>
	<view>
		<view>
			<view>收藏夹</view>
			<view>
				<scroll-view scroll-x="true" >
					<view>
						
					</view>
				</scroll-view>
			</view>
		</view>
		<view></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				history:[],
				data:{},
				idlist:[]
			}
		},
		onLoad(){
			let shoucangkey=uni.getStorageSync("shoucangkeyid")
			shoucangkey=shoucangkey.replace(/"/g,'')
			shoucangkey=shoucangkey.replace('[','')
			shoucangkey=shoucangkey.replace(']','')
			shoucangkey=shoucangkey.split(",")
			console.log(shoucangkey[0])
			for(let i=0;i<shoucangkey.length;i++){
				this.idlist.push(parseInt(shoucangkey[i]))
			}
			console.log(this.idlist,'666')
		},
		methods: {
			getidlist(){
				
			}
		}
	}
</script>

<style>

</style>
