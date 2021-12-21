<template>
	<!-- container -->
	<view :style="[tabBarContainerStyle]" class="tabBar_container">
		<!-- tab -->
		<view :style="{'width':width}" class="tab"
		v-for="(item,index) in tabs" :key="index">
			<uni-tag 
				:style="activeTabIndex===index?[tabActiveStyle]:[tabCommonStyle]"
				@tap="activeTagChange(index)"
				:type="activeTabIndex===index?activeType:commonType"
				:text="item"
				:size="size"
				circle="true"
				style="border: none;"></uni-tag>
		</view>
		<!-- slider -->
		<view v-if="showSlider" :style="[sliderStyle]" class="slider">
		</view>
	</view>
</template>

<script>
	export default {
		name: 'JinTagBar',
		props: {
			tabs: {
				type: Array,
				default: ['tab1', 'tab2', 'tab3']
			},
			size:{
				type:String,
				default:'defalut'
			},
			activeTabIndex: {
				type: Number,
				default: 0
			},
			backgroundColor: {
				type: String,
				default: '#FFFFFF'
			},
			borderBottom: {
				type: Boolean,
				default: false
			},
			borderTop: {
				type: Boolean,
				default: false
			},
			tabBarContainerCustomStyle: {
				type: Object,
				default: () => {
					return {}
				}
			},
			commonType: {
				type: String,
				default: 'default'
			},
			activeType: {
				type: String,
				default: 'primary'
			},
			commonFontSize: {
				type: Number,
				default: 20
			},
			activeFontSize: {
				type: Number,
				default: 20
			},
			showSlider: {
				type: Boolean,
				default: true
			},
			isFixed: {
				type: Boolean,
				default: false
			},
			offsetTop: {
				type: Number,
				default: 0
			}
		},
		data() {
			return {}
		},
		methods: {
			activeTagChange(index) {
				this.$emit('activeTagChange', index)
			}
		},
		computed: {
			tabBarContainerStyle() {
				let styleObj = {
					...this.tabBarContainerCustomStyle
				}
				styleObj.backgroundColor = this.backgroundColor

				if (this.borderBottom) {
					styleObj.borderBottom = '1px solid #DDD'
				}
				if (this.borderTop) {
					styleObj.borderTop = '1px solid #DDD'
				}
				if (this.isFixed) {
					styleObj.position = 'sticky'
					styleObj.zIndex = 99
					styleObj.top = this.offsetTop + 'rpx'
				} else {
					styleObj.position = 'relative'
				}

				return styleObj
			},
			tabCommonStyle() {
				let styleObj = {}
				styleObj.color = this.commonColor
				styleObj.fontSize = this.commonFontSize + 'rpx'
				styleObj.width = (710 / this.tabs.length) + 'rpx'
				return styleObj
			},
			tabActiveStyle() {
				let styleObj = {
					...this.tabCommonStyle
				}
				styleObj.color = this.activeColor
				styleObj.fontSize = this.activeFontSize + 'rpx'
				return styleObj
			},
			sliderStyle() {
				let styleObj = {}

				styleObj.width = (3 * this.activeFontSize) + 'rpx'
				styleObj.left =
					(20 + 710 / 2 / this.tabs.length - 3 * this.activeFontSize / 2) + (this.activeTabIndex * 710 / this
						.tabs.length) + 'rpx'

				return styleObj
			},
			width(){
				return (750/this.tabs.length) +'rpx'
			}
		}
	}
</script>

<style lang="scss" scoped>
	.tabBar_container {
		display: flex;
		justify-content: space-around;
		box-sizing: border-box;
		width: 100%;
		padding: 20rpx;
		align-items: center;

		.tab {
			box-sizing: border-box;
			text-align: center;
		}

		.slider {
			position: absolute;
			z-index: 0;
			bottom: 10rpx;
			// background-color: rgba(255,0,0,0.7) ;
			background-image: linear-gradient(to left, #ff557f, #ffaaff);
			height: 10rpx;
			transition: all 0.1s ease;
			border-radius: 10rpx;
		}
	}
</style>
