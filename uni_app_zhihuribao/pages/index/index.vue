<template>
	<view class="content">
		<view class="uni-list">
			
			 <swiper :indicator-dots="true"  :autoplay="true" :interval="3000" :duration="500">
            <swiper-item v-for="item in top_stories " :key="item" @tap="openinfo"
			 :data-newsid="item.id">
				<image :src="item.images" style="width: 100%;"></image>
            </swiper-item>
			</swiper>
			
			<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in list" :key="index" @tap="openinfo"
			 :data-newsid="item.id">
				<view class="uni-media-list">
					<image class="uni-media-list-logo" :src="item.images"></image>
					<view class="uni-media-list-body">
						<view class="uni-media-list-text-top">{{item.title}}</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [],
				top_stories: []
			};
		},
		onLoad: function() {

			uni.request({
				url: 'https://news-at.zhihu.com/api/4/news/latest',
				method: 'GET',
				success: res => {
					this.list = res.data.stories;
					this.top_stories = res.data.stories;
					
				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods: {
			openinfo(e) {
				var newsid = e.currentTarget.dataset.newsid;
				uni.navigateTo({
					url: '../info/info?newsid=' + newsid,
				});
			},
		}
	}
</script>

<style>
	.uni-media-list-body {
		height: auto;
	}

	.uni-media-list-text-top {
		line-height: 1.6em;
	}
</style>
