<template>
	<view class="market_container">
		market
		<!-- tab-bar -->
		<jin-tab-bar :tabs="tabs" :activeTabIndex="activeTabIndex" :activeFontSize="35"
			@activeTabChange="activeTabChange" :isFixed="isFixed"></jin-tab-bar>
		<!-- 滑动栏 -->
		<swiper 
			class="content_swiper"
			:current="activeTabIndex" 
			@change="activeSwiperChange"
			:style="{height:swiperHeight+'rpx'}"
			>
			<!-- 推荐 -->
			<swiper-item class="Recommand swiper-item">
				<!-- 下拉刷新滚动 -->
				<jin-scrolly 
					:dataSource="recommandList" 
					:trigger="recommandTrigger" 
					@refresherrefresh="handleRecommandRefresh"
					@refresherpulling="handleRecommandPulling"
					@scrolltolower="handleRecommandScrollEnd"
					>
					<!-- 特别插槽内容 -->
					<template slot="slot-0">
						<view class="scrollyItem">
							<view>
								<image style="height: 300rpx;" src="../../static/swipers/易方达基金.jpg" mode="widthFix"></image>
							</view>
							<view class="info_container">
								<uni-tag
									class="tag"
									size="mini"
									:text="'回顾'"
									type="primary"></uni-tag>
								<text class="info">{{'总公司电子商务部旗舰店'}}</text>
								<text class="info">{{'2000'}}阅读</text>
								<text class="info">{{'06:30'}}</text>
							</view>
						</view>
					</template>
				</jin-scrolly>
			</swiper-item>
			<!-- 要闻 -->
			<swiper-item class="mainNews">
				<jin-scrolly 
					:dataSource="mainNewsList" 
					:trigger="mainNewsTrigger"
					@refresherpulling="handleMainNewsPulling"
					@refresherrefresh="handleMainNewsRefresh"
				>
				</jin-scrolly>
			</swiper-item>
			<!-- 自选 -->
			<swiper-item class="mySelect swiper-item">
				<jin-tab-bar 
				:activeTabIndex="mySelectTabIndex"
				@activeTabChange="activeMySelectTabChange"
				:tabs="['全部','新闻','公告','研报']" 
				:commonFontSize="20"
				></jin-tab-bar>
				<swiper :current="mySelectTabIndex">
					<swiper-item>aaa</swiper-item>
					<swiper-item>bbb</swiper-item>
					<swiper-item>ccc</swiper-item>
					<swiper-item>ddd</swiper-item>
				</swiper>
			</swiper-item>
			<!-- 直播 -->
			<swiper-item class="live swiper-item"> 
				<view style="padding: 20rpx;">
					<view>
						精彩回顾
					</view>
					<view style="align-items: center;padding: 20rpx 0;position: relative;">
						<view :style="{
							backgroundColor:'rgba(0,0,0,0.5)',
							color:'white',
							fontSize:'20rpx',
							position: 'absolute',
							zIndex:'99',
							top:'40rpx',left: '20rpx'
							}">
							160567人观看
						</view>
						<view :style="{
							color:'white',
							position: 'absolute',
							zIndex:'99',
							top:'50%',left: '50%',
							transform:'translate(-50%,-50%)'
							}"
							>
							<image style="height: 100rpx;"
							src="../../static/icon/黑色/24gf-playCircle.png" mode="heightFix"></image>
						</view>
						<image 
						style="width: 100%;"
						src="../../static/content/精彩回顾.jpg" mode="widthFix">
						<view 
						style="background-color: #ddd;margin: 0;padding: 0;font-size: 28rpx;padding: 20rpx;"
						>乘风破浪开新篇，共话2022</view>
						</image>
					</view>
				</view>
				<view class="slash"></view>
				<view style="padding: 20rpx;">
					<view style="display: flex;justify-content: space-between;">
						<text>直播预告</text>
						<text style="font-size: 28rpx;color: #aaa;">直播日历 ></text>
					</view>
					<view style="display: flex;justify-content: space-between;align-items: center;">
						<view style="color: blue;width: 20%;font-size: 28rpx;">
							<view>15:00</view><view>今日</view>
						</view>
						<view style="overflow: hidden; text-overflow: ellipsis;white-space: nowrap;">
							共同富裕视角下的2022年宏观sfdfsfssfsdfsd
						</view>
						<view style="width: 20%;">
							<uni-tag text="预约" circle="true" type="primary"></uni-tag>
						</view>
					</view>
				</view>
				<view class="slash"></view>
				<view style="padding: 20rpx;">
					<view style="display: flex;justify-content: space-between;">
						<text>全部回看</text>
						<text style="font-size: 28rpx;color: blue;">我的</text>
					</view>
					<view style="margin: 20rpx 0 ;">
						<view style="font-size: 28rpx;">优选栏目</view>
						<scroll-view scroll-x="true" show-scrollbar="false">
							<view style="white-space: nowrap;margin: 20rpx 0;" >
								<uni-tag 
								style="margin-right: 20rpx;"
								v-for="(item,index) in ['基金超级碗','买卖双子星','投资训练营','金牌鉴股','投资理财','个股分析','市场分析','金融产品','其他']"
								:key="index"
								:text="item" type="primary"></uni-tag>
							</view>
						</scroll-view>
					</view>
					<view style="margin: 20rpx 0 ;">
						<view style="font-size: 28rpx;">近期回看</view>
						<scroll-view scroll-y="true">
							<jin-news-item 
							v-for="(x,index) in 100" :key="index"
							:item="{
								id:0,
								title:'乘风破浪开新篇，共话2022年投资新机遇',
								tag:'基金超级碗',
								tagType:'default',
								readNum:'161446'
							}"></jin-news-item>
						</scroll-view>
					</view>
				</view>
			</swiper-item>
			<!-- 课堂 -->
			<swiper-item>
				<view class="lesson_container" style="box-sizing: border-box;padding: 20rpx;">
					<view class="lesson_top" style="padding: 20rpx 0 ;">
						<view 
						style="background-image: linear-gradient(to right,#dcf1ff, #aaffff);border-radius: 10rpx;align-items: center;display: flex;justify-content: space-around;padding: 20rpx 0;">
							<view style="">aaa</view>
							<view>
								<view style="font-size: 28rpx;">用户名</view>
								<view style="font-size: 25rpx;color: #aaa;">投资需要不断学习</view>
							</view>
							<view style="color: #B3D4FA;font-size: 28rpx;">我的课程 ></view>
						</view>
						<view style="display: flex;justify-content: space-around;">
							<view v-for="(item,index) in ['全部课程','问答','投资词典']" :key="index">
								{{item}}
							</view>
						</view>
					</view>
					<view class="slash"></view>
					<jin-tag-bar 
					:activeTabIndex="activeLessonTagIndex"
					:showSlider="false"
					@activeTagChange="activeLessonTagChange"
					:tabs="['学习专题','优选课程','广发视点','短视频']"></jin-tag-bar>
					<view style="padding: 20rpx 0 ;">
						<view style="display: flex;flex-wrap: wrap;justify-content: space-between;">
							<view style="margin: 20rpx 0 ;">
								<image 
								style="width: 320rpx;height: 200rpx;"
								src="../../static/lesson/理财.jpg" mode=""></image>
								<view style="font-size: 28rpx;font-weight: bold;">标题：投顾选股方法</view>
								<view style="font-size: 18rpx;color: #aaa;">共2期 | 29744人学习</view>
							</view>
							<view style="margin: 20rpx 0 ;">
								<image 
								style="width: 320rpx;height: 200rpx;"
								src="../../static/lesson/基金定投.jpg" mode=""></image>
								<view style="font-size: 28rpx;font-weight: bold;">标题：投顾选股方法</view>
								<view style="font-size: 18rpx;color: #aaa;">共2期 | 29744人学习</view>
							</view>
							<view style="margin: 20rpx 0 ;">
								<image 
								style="width: 320rpx;height: 200rpx;"
								src="../../static/lesson/理论到实操.jpg" mode=""></image>
								<view style="font-size: 28rpx;font-weight: bold;">标题：投顾选股方法</view>
								<view style="font-size: 18rpx;color: #aaa;">共2期 | 29744人学习</view>
							</view>
							<view style="margin: 20rpx 0 ;">
								<image 
								style="width: 320rpx;height: 200rpx;"
								src="../../static/lesson/研判趋势.jpg" mode=""></image>
								<view style="font-size: 28rpx;font-weight: bold;">标题：投顾选股方法</view>
								<view style="font-size: 18rpx;color: #aaa;">共2期 | 29744人学习</view>
							</view>
						</view>
						<view style="text-align: center;font-size: 28rpx;color: #aaa;">更多课程 ></view>
					</view>
					<view class="slash"></view>
					
				</view>
			</swiper-item>
		</swiper>
		
	</view>
</template>

<script>
	export default {
		onPageScroll(e) {
			// console.log(e)
			if (e.scrollTop > 20) {
				this.isFixed = true
			} else {
				this.isFixed = false
			}
		},
		data() {
			return {
				// tab页签
				tabs: ['推荐', '要闻', '自选', '直播', '课堂','服务'],
				// 全局选中的tab索引
				activeTabIndex: 0,
				// 课程专题选中的tab索引
				activeLessonTagIndex:0,
				// 是否固定tab栏
				isFixed: false,
				swiperHeight:2200,
				// 推荐
				recommandList: [{
						id: '0',
						title: '新冠检测、生物疫苗概念拉升走高 兰卫医学、天瑞仪器等大涨。溢出溢出溢出溢出溢出溢出溢出溢出溢出溢出溢出溢出',
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
				recommandTrigger: false,
				isRecommandRefreshing: false,
				// 要闻
				mainNewsList: [{
						id: '0',
						title: '快讯：港股恒指低开0.49% 佳兆业集团复牌跌7.6%华人置业跌超31%',
						source: '新浪港股',
						time: '09:23'
					},
					{
						id: '1',
						title: '大盘延续震荡市，暂无趋势行情，不宜盲目追涨杀跌',
						source: '每日早盘必读',
						time: '09:11'
					},
					{
						id: '2',
						title: '创新产品层出不穷 公募FOF步入全球投资时代',
						source: '伤害证券报',
						time: '08:52'
					},
					{
						id: '3',
						title: '李秋喜到退休年龄 请辞山西汾酒董事长',
						source: '21世纪经济报道',
						time: '08:52'
					},
					{
						id: '4',
						title: '基本面趋好叠加需求回升 机构布局建材龙头股',
						source: '上海证券报',
						time: '08:51'
					}, {
						id: '5',
						title: '若千美元票据及利息应付未付，佳兆业将制定债务重组计划',
						source: '21世纪经济报道',
						time: '08:51'
					}, {
						id: '6',
						title: '发行市场升温 公募积极布局跨年行情',
						source: '上海证券报',
						time: '08:48'
					}
				],
				mainNewsTrigger: false,
				isMainNewsRefreshing: false,
				mySelectTabIndex:0,
			}
		},
		methods: {
			activeTabChange(index) {
				this.activeTabIndex = index
			},
			activeSwiperChange(e){
				this.activeTabChange(e.detail.current)
				this.$nextTick(()=>{
					this.enhandceSwiperHeight()
				})
			},
			enhandceSwiperHeight(){
				this.swiperHeight+=100
			},
			handleRecommandPulling() {
				this.recommandTrigger = true
			},
			handleRecommandRefresh() {
				if (this.isRecommandRefreshing) {
					return
				}
				this.isRecommandRefreshing = true
				setTimeout(() => {
					this.getRecommandList()
					this.recommandTrigger = false
					this.isRecommandRefreshing = false
				}, 3000)
			},
			getRecommandList() {
				this.recommandList = [{
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
			},
			handleMainNewsPulling(){
				this.mainNewsTrigger = true
			},
			handleMainNewsRefresh(){
				if (this.isMainNewsRefreshing) {
					return
				}
				this.isMainNewsRefreshing = true
				setTimeout(() => {
					this.getMainNewsList()
					this.mainNewsTrigger = false
					this.isMainNewsRefreshing = false
				}, 3000)
			},
			getMainNewsList(){
				let newMainNewsList=[{
						id: '7',
						title: '再次质疑734亿国有资产流失！健坤集团再声明：拟出售紫光部分资产抵债，点名这些A股投资人',
						source: '券商中国',
						time: '49分钟前'
					},
					{
						id: '8',
						title: '热搜第一！申通建议客户发顺丰',
						source: '券商中国',
						time: '49分钟前'
					},
					{
						id: '9',
						title: '又一家餐企陷困境！上海这家知名餐厅进入破产清算？双11还在推储值活动',
						source: '券商中国',
						time: '49分钟前'
					},
					{
						id: '10',
						title: '777家机构、1233个产品参赛！红塔证券“超越者杯”首届私募大赛圆满落幕，年度榜单重磅揭晓',
						source: '券商中国',
						time: '49分钟前'
					},
					{
						id: '11',
						title: '人民币中间价调贬282个基点，央行开展100亿元7天期和100亿元14天期逆回购操作',
						source: '第一财经',
						time: '08:07'
					}, {
						id: '12',
						title: '冬奥会即将举办，数字人民币迎来试点新场景，哪些个股将受益',
						source: '财联社',
						time: '09:34'
					}, {
						id: '13',
						title: '氢能源、电力板块受追捧，元宇宙个股分化，关注存量资金继续',
						source: '财联社',
						time: '09:33'
					}
				]
				this.mainNewsList = [...newMainNewsList,...this.mainNewsList,]
			},
			activeMySelectTabChange(index){
				this.mySelectTabIndex = index
			},
			activeLessonTagChange(index){
				this.activeLessonTagIndex = index
			}
		}
	}
</script>

<style lang="scss" scoped>
	.market_container {
		.content_swiper{
			.swiper-item{
				width: 100%;
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
		.slash {
			width: 100%;
			height: 15rpx;
			background-color: #B3D4FC;
			opacity: 0.3;
		}
	}
</style>
