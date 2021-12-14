<template>
	<view class="found_container">
		<!-- 头部搜索区 -->
		<view class="found_top">
			<uni-search-bar 
			class="search" :placeholder="currentKeyWord" 
			v-model="searchValue" 
				@confirm="search()"></uni-search-bar>
			<view class="letter">
				<text class="iconfont icon-xin"></text>
			</view>
		</view>
		<!-- 轮播图 -->
		<swiper class="swiper" indicator-dots autoplay circular>
			<swiper-item class="swiperItem" 
			v-for="item in swiperList" :key="item.id">
				<image :src="item.src" mode="widthFix"></image>
			</swiper-item>
		</swiper>
		<!--  -->
		<view class="selection">
			<view class="selectionItem" v-for="item in selectionList" :key="item.selectionId">
				<image :src="item.image"></image>
				<text>{{item.title}}</text>
			</view>
			
		</view>
		<!-- tab栏 -->
		<view class="found_navBar">
			推荐
		</view>
		<!--  -->
		<view class="found_show">
			利好消息
		</view>
	</view>
</template>

<script>
	// import UniSearchBar from '../../components/uni-search-bar/uni-search-bar.vue'
	export default {
		onLoad(){
			this.getSwiper()
			this.getSelection()
			this.getSearchKeyWords()
			this.intervalId = setInterval(()=>{
				if(this.currentKeyWordCount<this.searchKeyWords.length-1){
					this.currentKeyWordCount++
					this.currentKeyWord = this.searchKeyWords[this.currentKeyWordCount]
				}else{
					this.currentKeyWordCount=0
					this.currentKeyWord = this.searchKeyWords[this.currentKeyWordCount]
				}
			},3000)
		},
		onUnload(){
			clearInterval(this.intervalId)
			console.log('unload')
		},
		data() {
			return {
				intervalId:0,
				currentKeyWord:'',
				currentKeyWordCount:0,
				searchKeyWords:[],
				searchValue: '',
				swiperList:[],
				selectionList:[]
			}
		},
		methods: {
			search() {
				console.log("search")
			},
			getSwiper(){
				// 模拟获取数据
				this.swiperList = [
					{
						id:'001',
						src:'../../static/swipers/止损是什么意思.jpg'
					},
					{
						id:'002',
						src:'../../static/swipers/易方达基金.jpg'
					},
					{
						id:'003',
						src:'../../static/swipers/领体验金.jpg'
					}
				]
			},
			getSearchKeyWords(){
				this.searchKeyWords = [
					'把握碳中和红利',
					'一键打新',
					'问股选股'
				],
				this.currentKeyWord = this.searchKeyWords[0]
			},
			getSelection(){
				this.selectionList = [
					{
						selectionId:0,
						path:'',
						title:'咨询',
						image:'../../static/icon/黑色/zixun.png'
					},
					{
						selectionId:1,
						path:'',
						title:'新股申购',
						image:'../../static/icon/黑色/新.png'
					},
					{
						selectionId:2,
						path:'',
						title:'业务办理',
						image:'../../static/icon/黑色/chicangguanli.png'
					},
					{
						selectionId:3,
						path:'',
						title:'我要开户',
						image:'../../static/icon/黑色/tianjiayonghu.png'
					},
					{
						selectionId:4,
						path:'',
						title:'基金专区',
						image:'../../static/icon/黑色/jijin.png'
					},
					{
						selectionId:5,
						path:'',
						title:'股市天眼',
						image:'../../static/icon/黑色/小天眼.png'
					},
					{
						selectionId:6,
						path:'',
						title:'投顾专区',
						image:'../../static/icon/黑色/guanyuguwen.png'
					},
					{
						selectionId:7,
						path:'',
						title:'金牌鉴股',
						image:'../../static/icon/黑色/jinpai.png'
					},
					{
						selectionId:8,
						path:'',
						title:'持仓查询',
						image:'../../static/icon/黑色/查询.png'
					},
					{
						selectionId:9,
						path:'',
						title:'全部',
						image:'../../static/icon/黑色/quanbu-copy.png'
					}
				]
			}
		}
	}
</script>

<style lang="scss">
	.found_container {
		.found_top {
			display: flex;
			.search {
				width: 650rpx;
			}

			.letter {
				width: 100rpx;
				box-sizing: border-box;
				padding: 8px 8px 8px 0px;
				text-align: center;
				align-items: center;
				text {
					font-size: 50rpx;
					line-height: 36px;
				}
			}
		}
		.swiper{
			box-sizing: border-box;
			padding: 0px 8px;
			.swiperItem{
				align-items: center;
				image{
					width: 100%;
				}
			}
		}
		.selection{
			margin: 30rpx 0 ;
			display: flex;
			justify-content: space-around;
			flex-wrap: wrap;
			.selectionItem{
				margin: 20rpx 0rpx;
				width: 20%;
				display: flex;
				align-items: center;
				text-align: center;
				flex-direction: column;
				image{
						width: 40rpx;
						height: 40rpx;
				}
				text{
					line-height: 40rpx;
					font-size: 25rpx;
				}
			}
		}
	}
</style>
