<template>
	<!-- 容器 -->
	<view class="scrolly_container">
		<!-- 可下拉刷新容器 -->
		<scroll-view 
			refresher-enabled
			:refresher-triggered="trigger"
			@refresherpulling="refresherpulling"
			@refresherrefresh="refresherrefresh"
			class="scrolly"
			scroll-y="true"
			>
		<!-- 内容 -->
			<view v-for="(item,index) in dataSource" :key="item.id">
				<jin-news-item 
					:item="item">
				</jin-news-item>
				<!-- 自定义内容的插槽 -->
				<!-- #ifdef MP -->
				<slot name="slot-{{index}}"></slot>
				<!-- #endif -->
				<!-- #ifdef H5|| APP-PLUS -->
				<slot :name="'slot-'+index"></slot>
				<!-- #endif -->
			</view>
		</scroll-view>
	</view>
</template>

<script>
	import UniTag from'../uni-tag/uni-tag.vue'
	export default {
		name:'JinScrolly',
		props:{
			dataSource:{
				type:Array,
				default:()=>{
					return []
				}
			},
			itemFontSize:{
				type:Number,
				default:28
			},
			trigger:{
				type:Boolean,
				default:false
			}
		},
		methods:{
			refresherpulling(e){
				this.$emit('refresherpulling',e)
			},
			refresherrefresh(e){
				this.$emit('refresherrefresh',e)
			}
		},
		components:{
			'uni-tag':UniTag
		}
	}
</script>

<style lang="scss" scoped>
	.scrolly_container{
		.scrolly{
			box-sizing: border-box;
			padding: 20rpx;
		}
	}
</style>
