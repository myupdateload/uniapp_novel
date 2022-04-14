<template>
	<view class="content" :style="{'color':fontcolor,'backgroundColor':bakgroundcolor}">
		<button @click="showDrawer" class="show" ><image  src="../../static/read/agreement.png" style="height: 40rpx;width: 40rpx;"></image></button>
				<uni-drawer ref="showRight" mode="right" :mask-click="true">
					<scroll-view style="height: 100%;" scroll-y="true" class="big-draw">
					<!-- 	<button class="btn2" @click="closeDrawer" >X</button> -->
						<view :class="number===index?'draw1':'draw'" ref="mulu"  v-for="(item,index) in chapterdata" :key="index"  @click="jump(index)" >
							{{item.chaperIdx}} {{item.name}}
						</view>
					</scroll-view>
				</uni-drawer>
		<button @click="showDrawer2"  class="show2" ><image  src="../../static/read/setting.png" style="height: 40rpx;width: 40rpx;"></image></button>
				<uni-drawer  ref="showRight2" mode="right" :mask-click="true">
					<scroll-view style="height: 100%;" scroll-y="true" class="big-draw2">
						<!-- <button class="btn22" @click="closeDrawer2" >X</button> -->
						<view class="draw2"></view>
						<view class="twos">
							<view>白天模式</view>
							<view class="uni-padding-wrap uni-common-mt">
										<view class="switch" >
											<switch checked="false" @change="switch1Change" color="#87CEFA" />	
										</view>
									</view>
						</view>
						<view>
							<view class="three">字体大小</view>
							<view class="big-btn">
								<button class="btnstyle" @click="btnstyle1">+</button>
								<button class="btnstyle" @click="btnstyle2">默认</button>
								<button class="btnstyle" @click="btnstyle3">-</button>
							</view>
						</view>
						<view class="btnbuttom">
							<button class="btns1" @click="btns1">上一章</button>
							<button class="btns2" @click="btns2">下一章</button>
						</view>
					</scroll-view>
				</uni-drawer>
		
		<scroll-view   class="scroll" scroll-y="true" :style="{'backgroundColor':bakgroundcolor}">
			<view  class="views" v-for="(item,index) in readinfo" :style="{fontSize:fontsize+'rpx'}">
					<text >{{item.content}}</text>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				readdata:[],//一个数组  0为书的id,1为点击的章节
				readinfo:[],
				number:0,
				chapterdata:[],	//目录
				fontsize:40,
				fontcolor:'black',
				bakgroundcolor:'#F5F5DC',
				judge:true,
				muluselected:false
			}
		},
		async onLoad(id){  
			const datas=JSON.parse(id.content)
			this.readdata=datas   //拿到书的id与章节
			const res = await uni.request({
				url:'http://39.96.77.250/view/chapters?&bookId='+this.readdata[0],//获取小说的章节供抽屉使用
			})
			
			this.chapterdata=res[1].data.result //把章节数据存在数组中
			
			this.getread()//加载页面小说部分数据
		},
		onReachBottom(){
			this.number=this.number+3
			this.getread()
			},
		methods: {
			btns1(){
				this.number--,
				this.readinfo=[]
				this.getread()
			},
			btns2(){
				this.number++
				this.readinfo=[]
				this.getread()
			},
			switch1Change(){
				if(this.judge===false){
					this.fontcolor='black',
					this.bakgroundcolor='#F5F5DC',
					this.judge=!this.judge,
					console.log(this.bakgroundcolor)
				}
				else{
					this.fontcolor='white',
					this.bakgroundcolor='#2E2E2E',
					this.judge=!this.judge,
					console.log(this.bakgroundcolor)
				}
				
			},
			btnstyle1(){
				this.fontsize=this.fontsize+5
			},
			btnstyle2(){
				this.fontsize=40
			},
			btnstyle3(){
				this.fontsize=this.fontsize-5
			},
			showDrawer() {
							this.$refs.showRight.open();
						},
						closeDrawer() {
							this.$refs.showRight.close();
						},
			showDrawer2(){
				this.$refs.showRight2.open();
			},
			jump(index){
				this.number=index,
				this.readinfo=[]
				this.readdata[1]=1
				this.getread()
			},
			async getread(){
				const res = await uni.request({
					url:'http://39.96.77.250/view/readBook?&bookId='+this.readdata[0]+'&chapterId='+(this.readdata[1]+this.number),
					//获取某一章节内容，得到三个数组为三个整章节
				})
				console.log(this.readdata[1])
				console.log(res)
				
				this.readinfo=[...this.readinfo,...res[1].data.result]
				console.log(this.readinfo)
			}
		}
	}
</script>

<style lang="scss">
	.content{
		background-color: #F5F5DC;
		height: 100%;
		width: 100%;
	}
	
	.twos{
		margin-top: 100rpx;
	}
	.three{
		margin-top: 100rpx;
	}
	.big-btn{
		display: flex;
		flex-direction: row;
	}
	.btnstyle{
		height: 80rpx;
		width: 160rpx;
		background-color: #87CEFA;
		color: blue;
		
	}
	.btnbuttom{
		display: flex;
		flex-direction: row;
		margin-top: 100rpx;
	}
	.btns1{
			height: 100rpx;
			width: 250rpx;
			background-color: #87CEFA;
			color: blue;
			margin-bottom: 0;
			margin-left: 10rpx;
		}
	.btns2{
			height: 100rpx;
			width: 250rpx;
			background-color: #87CEFA;
			color: blue;
			margin-bottom: 0;
			margin-right: 10rpx;
		}
	.show{
		position: fixed;
		height: 100rpx;
		width: 100rpx;
		z-index: 99;
		margin-top: 100rpx;
		margin-left: 90%;
		background-color: #87CEFA;
		color: blue;
		opacity: 0.3;
	}
	.show2{
		position: fixed;
		height: 100rpx;
		width: 100rpx;
		z-index: 99;
		margin-top: 200rpx;
		margin-left: 90%;
		background-color: #87CEFA;
		color: blue;
		opacity: 0.3;
	}
	.big-draw2{
		background-color:#F5F5DC ;
	}
	.big-draw{
		background-color:#F5F5DC ;
		
		.draw{
			border: 3rpx solid #3F536E;
		}
		 .draw1{
		 	border: 3rpx solid #3F536E;
			color: red;
		 }
		
	}
	.views{
		margin-left: 15rpx;
		margin-right: 15rpx;
		
	}
	.scroll{
		background-color: #F5F5DC;
		height: 100%;
		width: 100%;
	}
</style>
