<template>
	<view>
		<view :style="[newsItemStyle]" class="newsItem">
			<view class="newsItem_left">
				<text v-if="item.title" class="title">
					{{item.title}}
				</text>
				<view class="info_container">
					<uni-tag class="tag" v-if="item.tag" size="mini" :text="item.tag" :type="item.tagType"></uni-tag>
					<text class="info" v-if="item.source">{{item.source}}</text>
					<text class="info" v-if="item.readNum">{{item.readNum}}阅读</text>
					<text class="info" v-if="item.time">{{item.time}}</text>
				</view>
			</view>
			<view v-if="item.img" class="newsItem_right">
				{{item.img}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: "JinNewsItem",
		props: {
			itemFontSize:{
				type:Number,
				default:28
			},
			item:Object,
		},
		data() {
			return {

			};
		},
		computed:{
			newsItemStyle(){
				let styleObj = {}
				styleObj.fontSize = this.itemFontSize + 'rpx'
				return styleObj
			}
		}
	}
</script>

<style lang="scss">
	.newsItem {
		box-sizing: border-box;
		padding: 20rpx;
		background-color: white;
		border-bottom: 1px solid #ddd;
		display: flex;

		.newsItem_left {
			// border: 1px solid red;
			overflow: hidden;
			width: 100%;
			.title {
				overflow: hidden;
				text-overflow: ellipsis;
				display: -webkit-box;
				-webkit-line-clamp:2;
				-webkit-box-orient:vertical;
			}

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

		.newsItem_right {
			// border: 1px solid red;
			// width: 30%;
			width: 30%;
			height: 100%;
		}
	}
</style>
