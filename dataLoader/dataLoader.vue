<template>
	<div class="data-loader" :class="{loading: loading}">
		<i></i>
		<span>{{ message }}</span>
	</div>
</template>
<script>

	export default {
		name: 'DataLoader',
		props: {
			distance: {
				type: Number,
				default: 0,
			},
			getData: {
				type: Function,
				required: true,
			},
			messageMap: {
				type: Object,
				default() {
					return {
						initial: '上拉加载更多数据',
						loading: '正在努力加载数据...',
						loaded: '没有更多数据了~',
					};
				},
			},
		},
		data() {
			return {
				page: 1,
				loading: false,
				loaded: false,
				message: null,
			};
		},
		mounted() {
			this.loadData();
			window.addEventListener('scroll', this.scrollHandler);
		},
		beforeDestroy() {
			window.removeEventListener('scroll', this.scrollContainer);
		},
		methods: {
			loadData() {
				this.loading = true;
				this.message = this.messageMap.loading;
				this.getData(this.page, this.loadDataCallback);
			},
			scrollHandler() {
				if (this.loading || this.loaded) {
					return;
				}
				if (document.documentElement.scrollHeight - window.innerHeight - window.scrollY > this.distance) {
					return;
				}
				this.loadData();
			},
			loadDataCallback(loaded) {
				this.loading = false;
				if (typeof loaded === 'string') { // 出错了，传递出错提示信息
					this.message = loaded;
				} else if (loaded) {
					this.loaded = true;
					this.message = this.messageMap.loaded;
				} else {
					this.page += 1;
					this.message = this.messageMap.initial;
				}
			},
			reload() {
				this.loaded = false;
				this.page = 1;
				this.loadData();
			},
		},
	};
</script>
<style lang="less" scoped>
	.data-loader {
		font-size: 0;
		line-height: 20px;
		text-align: center;
		>i {
			display: none;
			vertical-align: top;
			margin: 2px 5px 0 0;
		}
		>span {
			display: inline-block;
			vertical-align: top;
			font-size: 12px;
			color: #ccc;
		}
		&.loading {
			>i {
				display: inline-block;
			}
		}
	}
</style>