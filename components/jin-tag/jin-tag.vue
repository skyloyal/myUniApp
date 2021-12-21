<template>
	<text 
		class="jin-tag" 
		v-if="text" 
		:class="classes"
		@click="onClick">
		{{text}}
	</text>
</template>

<script>
	export default {
		name:"JinTag",
		props:{
			text:String,
			disabled: {
				// 是否为禁用状态
				type: [Boolean, String],
				default: false
			},
		},
		data() {
			return {
				
			};
		},
		computed:{
			classes(){
				const {
					type,
					disabled,
					inverted,
					circle,
					mark,
					size,
					isTrue
				} = this
				const classArr = []
				return classArr.join(' ')
			}
		},
		methods:{
			onClick(){
				this.$emit('click')
			}
		}
	}
</script>

<style>
	.jin-tag{
		border-radius: 5rpx;
		&--disabled {
			opacity: 0.5;
			/* #ifdef H5 */
			cursor: not-allowed;
			/* #endif */
		}
	}
</style>
