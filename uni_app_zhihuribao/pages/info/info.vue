<template>
	<view class="content">
		<view><image class="uni-media-list-logo" :src="imgage" style="width: 400px;height: 400px;"></image></view>
		<view class="title">{{title}}</view>
		<view class="art-content">
			<rich-text class="richText"  :nodes="strings"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return{
				title:'',
				strings:'',
				imgage:''
			}	
		},
		onLoad:function(e){
			uni.request({
				url: 'http://news-at.zhihu.com/api/2/news/'+e.newsid,
				method: 'GET',
				data: {},
				success: res => {
					this.title=res.data.title;
					this.strings=res.data.body.replace("type=“text/javascript”",'type="text/javascript"');
					this.imgage=res.data.image;
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}

</script>

<style>
.content{padding: 10upx 2%; width: 96;flex-wrap: wrap;}
.title{line-height: 2em;font-weight: 700;font-size: 38upx;}
.art-content{line-height: 2e}
.uni-media-list-logo{width: 400px;height: 400px;}
</style>
