<template>
	<view class="found_container">
		<!-- 头部搜索区 -->
		<view class="found_top">
			<uni-search-bar class="search" :placeholder="currentKeyWord" v-model="searchValue" @confirm="search()">
			</uni-search-bar>
			<view class="letter">
				<text class="iconfont icon-xin"></text>
			</view>
		</view>
		<!-- 轮播图 -->

		<swiper class="found_swiper" indicator-dots autoplay circular>
			<swiper-item class="swiperItem" v-for="item in swiperList" :key="item.id">
				<image :src="item.src" mode="widthFix"></image>
			</swiper-item>
		</swiper>
		<!-- 选项 -->
		<view class="found_selection">
			<view @click="goToAnotherPage(item.url)" class="selectionItem" v-for="item in selectionList"
				:key="item.selectionId">
				<image :src="item.image"></image>
				<text>{{item.title}}</text>
			</view>

		</view>
		<view class="found_slash"></view>
		<!-- tab栏 -->
		<jin-tab-bar :tabs="tabs" :activeTabIndex="activeTabIndex" :activeFontSize="35"
			@activeTabChange="activeTabChange" :offsetTop="offsetTop" :isFixed="isTabFixed"></jin-tab-bar>
		<!-- 滑动栏 -->
		<swiper :current="activeTabIndex" @change="activeSwiperChange">
			<swiper-item>aaa</swiper-item>
			<swiper-item>bbb</swiper-item>
			<swiper-item>ccc</swiper-item>
		</swiper>
		<!-- 推荐列表 -->
		<jin-scrolly 
			:dataSource="subscribeList" 
			:trigger="subscribeTrigger" 
			@refresherrefresh="handleSubscribeListRefresh"
			@refresherpulling="handleSubscribeListPulling">
			<!-- 自定义新闻 -->
			<template slot="slot-0">
				<view class="scrollyItem">
					<view>
						<image style="height: 300rpx;" src="../../static/swipers/易方达基金.jpg" mode="widthFix"></image>
					</view>
					<view class="info_container">
						<uni-tag class="tag" size="mini" :text="'回顾'" type="primary"></uni-tag>
						<text class="info">{{'总公司电子商务部旗舰店'}}</text>
						<text class="info">{{'2000'}}阅读</text>
						<text class="info">{{'06:30'}}</text>
					</view>
				</view>
			</template>
			<template slot="slot-3">
				<view class="scrollyItem">
					<view>
						<image style="height: 300rpx;" src="../../static/content/如何理解2021年股票行情的持续回落.png" mode="widthFix"></image>
					</view>
					<view class="info_container">
						<uni-tag class="tag" size="mini" :text="'重磅消息'" type="warning"></uni-tag>
						<text class="info">{{'广发发'}}</text>
						<text class="info">{{'21万'}}点击量</text>
						<text class="info">{{'06:30'}}</text>
					</view>
				</view>
			</template>
		</jin-scrolly>
	</view>
	</view>
</template>

<script>
	export default {
		onLoad() {
			console.log('onload')
			this.init()
		},
		onUnload() {
			clearInterval(this.intervalId)
			console.log('unload')
		},
		onPageScroll(e) {
			console.log(e)
			this.scrollTop = e.scrollTop
			if (e.scrollTop > this.tabInitPosition) {
				this.isTabFixed = true
			} else {
				this.isTabFixed = false
			}
		},
		data() {
			return {
				// 当前页面竖向位置
				scrollTop: 0,
				// tab栏初始竖向位置
				tabInitPosition:294,
				// 搜索框轮换placeholder
				intervalId: 0,
				// 搜索框轮换placeholder值
				currentKeyWord: '',
				// 搜索框轮换placeholder序号
				currentKeyWordCount: 0,
				// 搜索框轮换placeholder值列表
				searchKeyWords: [],
				// 搜索框值
				searchValue: '',
				// 轮播图列表
				swiperList: [],
				// 选项列表
				selectionList: [],
				// tab选项
				tabs: ['推荐', '要闻', '自选', '直播', '课堂', '服务'],
				// tab栏选中id
				activeTabIndex: 0,
				// tab是否固定
				isTabFixed: false,
				// 固定位置距离顶部
				offsetTop: 104,
				subscribeList: [{
						id: '0',
						title: '新冠检测、生物疫苗概念拉升走高 兰卫医学、天瑞仪器等大涨',
						source: '证券时报',
						tag: '置顶',
						tagType: 'error',
						readNum: '1203',
						time: '09:54'
					},
					{
						id: '1',
						title: '两部门：加快新能源汽车推广应用  加快充电桩、换电站等配套设施建设',
						source: 'e公司',
						tag: '要闻',
						tagType: 'error',
						readNum: '5555',
						time: '11:23'
					},
					{
						id: '2',
						title: '千亿级新风口？电解水制氢空间巨大，布局公司名单出炉，北上资金拿下10%筹码，大手笔加仓4股',
						source: '证券时报',
						tag: '概念',
						tagType: 'primary',
						readNum: '3307',
						time: '13:08'
					},
					{
						id: '3',
						title: '深夜重磅！"网信国家队"突然放大招，旗下7家A股公司股权划转！',
						source: '证券时报',
						tag: '重磅',
						tagType: 'primary',
						time: '08:07'
					},
					{
						id: '4',
						title: '深夜重磅！"网信国家队"突然放大招，旗下7家A股公司股权划转！',
						source: '证券时报',
						tag: '重磅',
						tagType: 'primary',
						time: '08:07'
					}, {
						id: '5',
						title: '深夜重磅！"网信国家队"突然放大招，旗下7家A股公司股权划转！',
						source: '证券时报',
						tag: '重磅',
						tagType: 'primary',
						time: '08:07'
					}, {
						id: '6',
						title: '深夜重磅！"网信国家队"突然放大招，旗下7家A股公司股权划转！',
						source: '证券时报',
						tag: '重磅',
						tagType: 'primary',
						time: '08:07'
					}
				],
				subscribeTrigger: false,
				subscribeIsRrfreshing:false
			}
		},
		methods: {
			// 初始化
			init() {
				this.getSwiper()
				this.getSelections()
				this.getSearchKeyWords()
				if (this.intervalId !== 0) {
					clearInterval(this.intervalId)
				}
				this.intervalId = setInterval(() => {
					if (this.currentKeyWordCount < this.searchKeyWords.length - 1) {
						this.currentKeyWordCount++
						this.currentKeyWord = this.searchKeyWords[this.currentKeyWordCount]
					} else {
						this.currentKeyWordCount = 0
						this.currentKeyWord = this.searchKeyWords[this.currentKeyWordCount]
					}
				}, 3000)
			},
			// 搜索
			search() {
				console.log("search")
			},
			// 获取轮播图
			getSwiper() {
				// 模拟获取数据
				this.swiperList = [{
						id: '001',
						src: '../../static/swipers/止损是什么意思.jpg'
					},
					{
						id: '002',
						src: '../../static/swipers/易方达基金.jpg'
					},
					{
						id: '003',
						src: '../../static/swipers/领体验金.jpg'
					}
				]
			},
			// 获取搜索框关键字列表
			getSearchKeyWords() {
				this.searchKeyWords = [
						'把握碳中和红利',
						'一键打新',
						'问股选股'
					],
					this.currentKeyWord = this.searchKeyWords[0]
			},
			// 获取选项列表
			getSelections() {
				this.selectionList = [{
						selectionId: 0,
						url: '',
						title: '咨询',
						image: '../../static/icon/黑色/zixun.png'
					},
					{
						selectionId: 1,
						url: '',
						title: '新股申购',
						image: '../../static/icon/黑色/新.png'
					},
					{
						selectionId: 2,
						url: '',
						title: '业务办理',
						image: '../../static/icon/黑色/chicangguanli.png'
					},
					{
						selectionId: 3,
						url: '',
						title: '我要开户',
						image: '../../static/icon/黑色/tianjiayonghu.png'
					},
					{
						selectionId: 4,
						url: '',
						title: '基金专区',
						image: '../../static/icon/黑色/jijin.png'
					},
					{
						selectionId: 5,
						url: '',
						title: '股市天眼',
						image: '../../static/icon/黑色/小天眼.png'
					},
					{
						selectionId: 6,
						url: '',
						title: '投顾专区',
						image: '../../static/icon/黑色/guanyuguwen.png'
					},
					{
						selectionId: 7,
						url: '',
						title: '金牌鉴股',
						image: '../../static/icon/黑色/jinpai.png'
					},
					{
						selectionId: 8,
						url: '',
						title: '持仓查询',
						image: '../../static/icon/黑色/查询.png'
					},
					{
						selectionId: 9,
						url: '',
						title: '全部',
						image: '../../static/icon/黑色/quanbu-copy.png'
					}
				]
			},
			// 导航链接
			goToAnotherPage(url) {
				console.log('正在跳转至', url)
			},
			// 点击tab选项变化
			activeTabChange(index) {
				this.activeTabIndex = index
				if(this.scrollTop>this.tabInitPosition){
					uni.pageScrollTo({
						scrollTop:this.tabInitPosition,
						duration:300
					})
				}
			},
			// 滑动tab选项变化
			activeSwiperChange(e){
				this.activeTabChange(e.detail.current)
			},
			// 推荐下拉刷新
			handleSubscribeListPulling() {
				this.subscribeTrigger = true
			},
			// 推荐下拉刷新
			handleSubscribeListRefresh() {
				if (this.subscribeIsRrfreshing) {
					return
				}
				this.subscribeIsRrfreshing = true
				setTimeout(() => {
					this.getScribeList()
					this.subscribeTrigger = false
					this.subscribeIsRrfreshing = false
				}, 3000)
			},
			// 获取推荐列表
			getScribeList() {
				this.subscribeList = [{
						id: '0',
						title: '1300亿基金“顶流”，2022年更考研基金经理的眼光',
						source: '中国基金报',
						tag: '基金',
						tagType: 'error',
						readNum: '573',
						time: '08:29'
					},
					{
						id: '1',
						title: '刚刚！证监会重磅出售，精准狙击“假外资”！哪些资金最受冲击？设置一年过渡期，一年后只卖不买',
						source: '券商中国',
						tag: '要闻',
						tagType: 'error',
						readNum: '3020',
						time: '00:00'
					},
					{
						id: '2',
						title: '震惊！这国股市突然崩盘，1小时熔断2次，被迫紧急叫停交易，发生了什么？美股道指大跌超530点',
						source: '券商中国',
						tag: '关注',
						tagType: 'primary',
						readNum: '4682',
						time: '09:49'
					},
					{
						id: '3',
						title: '保险',
						source: '券商中国',
						tag: '保险',
						tagType: 'primary',
						time: '08:07'
					},
					{
						id: '4',
						title: '年内26家上市公司',
						source: '证券时报',
						time: '08:07'
					}, {
						id: '5',
						title: '深夜重磅！"网信国家队"突然放大招，旗下7家A股公司股权划转！',
						source: '证券时报',
						tag: '重磅',
						tagType: 'primary',
						time: '08:07'
					}, {
						id: '6',
						title: '深夜重磅！"网信国家队"突然放大招，旗下7家A股公司股权划转！',
						source: '证券时报',
						tag: '重磅',
						tagType: 'primary',
						time: '08:07'
					}
				]
			}
		}
	}
</script>

<style lang="scss" scoped>
	.found_container {

		// 顶部搜索栏、信息
		.found_top {
			background-color: white;
			width: 100%;
			position: sticky;
			z-index: 1;
			top: 0;
			display: flex;

			.search {
				width: 90%;
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

		// 轮播图
		.found_swiper {
			// margin-top: 104rpx;
			box-sizing: border-box;
			padding: 0px 8px;

			.swiperItem {
				align-items: center;

				image {
					width: 100%;
				}
			}
		}

		// 选项
		.found_selection {
			margin: 30rpx 0 0 0;
			display: flex;
			justify-content: space-around;
			flex-wrap: wrap;

			.selectionItem {
				margin: 20rpx 0rpx;
				width: 20%;
				display: flex;
				align-items: center;
				text-align: center;
				flex-direction: column;

				image {
					width: 40rpx;
					height: 40rpx;
				}

				text {
					line-height: 40rpx;
					font-size: 25rpx;
				}
			}
		}

		// 分隔栏
		.found_slash {
			width: 100%;
			height: 15rpx;
			background-color: #B3D4FC;
			opacity: 0.3;
		}

	}

	// 插槽样式
	.scrollyItem {
		box-sizing: border-box;
		padding: 20rpx;
		background-color: white;
		border-bottom: 1px solid #ddd;

		.info_container {
			align-items: center;
			margin: 20rpx 0 0 0;
			display: flex;

			.tag {
				margin-right: 20rpx;
				border-radius: 10rpx;
			}

			.info {
				font-size: 20rpx;
				margin-right: 20rpx;
				color: #aaa;
			}
		}
	}
</style>
