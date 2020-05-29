<template>
	<view class="content">
		<view class="status_bar">
		        <!-- 这里是状态栏 当navigationStyle设为custom或titleNView设为false时，
				原生导航栏不显示非H5端，手机顶部状态栏区域会被页面内容覆盖。这是因为窗体是沉浸式的原因 
				状态栏高度的css变量--status-bar-height  https://ext.dcloud.net.cn/plugin?id=52  这个前端导航栏自动处理了状态栏高度占位问题-->
		</view>
		<!-- 顶部搜索 -->
		<view class="contentBox"> 
		<!-- <uni-nav-bar left-icon="back" left-text="返回" right-text="菜单" title="导航栏组件" class="fixed"></uni-nav-bar> -->

	<view class="contentBox-titleFiex">
		<!-- 搜索 -->
<!-- 		<view class="contentBox-titleFiex-input">
			<div class="contentBox-titleFiex-input-box">
				<text class="lg text-gray cuIcon-search"></text>
				白菜
			</div>
		</view> -->
	</view>
		<!-- 轮播图 -->
		<scroll-view scroll-y="true" class="scroll-Y" :upper-threshold='50' :lower-threshold='50'>
			<swiper class="screen-swiper square-dot" :indicator-dots="true" :circular="true" :autoplay="true" interval="5000"
			 duration="500">
				<swiper-item v-for="(item,index) in swiperList" :key="index">
					<image :src="item.url" mode="aspectFill" v-if="item.type=='image'"></image>
					<video :src="item.url" autoplay loop muted :show-play-btn="false" :controls="false" objectFit="cover" v-if="item.type=='video'"></video>
				</swiper-item>
			</swiper>
			<!-- 导航 -->
			<view class="bg-white">
				<view class="cu-list grid col-5 no-border">
					<view class="cu-item" v-for="(item,index) in cuIconList" :key="index">
						<view :class="['cuIcon-' + item.cuIcon,'text-' + item.color]">
							<view class="cu-tag badge" v-if="item.badge!=0">
								<block v-if="item.badge!=1">{{item.badge>99?'99+':item.badge}}</block>
							</view>
						</view>
						<text>{{item.name}}</text>
					</view>
				</view>
				<!-- 会员卡 -->
				<view class="Index-vip">
					<view class="Index-vip-list">
						<view class="Index-vip-list-icon">
							<text class="lg text-gray cuIcon-crownfill"></text>
						</view>
						<view class="Index-vip-list-text">
							<text>加入绿卡会员<text style="color: #FFFFFF;" class="lg text-gray cuIcon-title"></text>预计每年节省806元</text>
						</view>
						<view class="Index-vip-list-right">
							5折开卡<text style="color: #FFFFFF;" class="lg text-gray cuIcon-right"></text>
						</view>
					</view>
				</view>
				<!-- 今日疯抢 -->
				<view class="Index-Rush">
					<view class="Index-Rush-left">
						<text style="color: #3ECD60;" class="lg text-gray cuIcon-titles"></text>
						<text>今日疯抢</text>
						<view class="shoping-buy-right">
							<text class="shoping-buy-right-time">00</text>
							<text>:</text>
							<text class="shoping-buy-right-time">00</text>
							<text>:</text>
							<text class="shoping-buy-right-time">00</text>
						</view>
					</view>
				</view>
				<!-- 超出部分滚动显示 -->
				<scroll-view class="scroll-view_H" scroll-x="true">
						<view class="scroll-view-H-Box">
							<view class="scroll-view-item_H" v-for="(item,index) in Insane" :key='index'>
								<!-- 图片 -->
								<view class="scroll-view-item_H-img">
									<image :src="item.propaganda"></image>
								</view>
								<!-- 配文 -->
								<view class="scroll-view-item_H-name">
									{{item.name}}
								</view>
								<!-- 购物和价格 -->
								<view class="scroll-view-item_H-news">
									<view class="scroll-view-item_H-news-left">
										<view class="scroll-view-item_H-news-left-top">
											￥{{ item.vip_price > 0 ? item.vip_price : item.price}}
										</view>
										<view class="scroll-view-item_H-news-left-bottom" v-show="item.vip_price > 0">
											￥{{item.price}}
										</view>
									</view>
									<view class="scroll-view-item_H-news-right">
										<text class="lg text-gray cuIcon-cart"></text>
									</view>
								</view>
							</view>
						</view>
				</scroll-view>
				
			</view>
		</scroll-view>
		<!-- 猜你喜欢 -->
		<view class="Index-Rush">
			<view class="Index-Rush-left">
				<text style="color: #3ECD60;" class="lg text-gray cuIcon-titles"></text>
				<text>猜你喜欢</text>
			</view>
		</view>
		<!-- 猜你喜欢  内容-->
		<view class="Index-live">
			<!-- 列表 -->
			<view class="Index-live-list"  v-for="(item,index) in homeLiveAll" :key="index">
				<!-- 图片 -->
				<view class="Index-live-list-img" @click="toShoping(item.id)">
					<!-- <image src="https://ddimg.ddxq.mobi/02a7557cb9ab1503365698396.jpg!maicai.product.list"></image> -->
					<image src="http://img.nodebook.top/2020_02_27_04_25_1496548image/jpeg"></image>
				</view>
				<!-- 文字 -->
				<view class="Index-live-list-text" @click="toShoping(item.id)">
					土鸡蛋 8 枚 
				</view>
				<!-- 购物车和价格 -->

			</view>
		</view>
	</view>
	</view>
</template>

<script>
	import {uniNavBar } from '@dcloudio/uni-ui'

	export default {
		components: {
			uniNavBar
		},
		data() {
			return {
				Insane: [{
						"id": 8,
						"name": "清美水晶冰爽 230g/杯",
						"price": "2.50",
						"vip_price": "0.00",
						"propaganda": "http://img.nodebook.top/2020_02_27_04_28_105536image/jpeg"
					},
					{
						"id": 9,
						"name": "旭洋麻腐 350g/盒",
						"price": "4.90",
						"vip_price": "0.00",
						"propaganda":"http://img.nodebook.top/2020_02_27_04_28_105536image/jpeg"
					},
					{
						"id": 25,
						"name": "爱森五花肉 500g",
						"price": "46.90",
						"vip_price": "0.00",
						"propaganda":"http://img.nodebook.top/2020_02_27_04_28_105536image/jpeg"
					},
					{
						"id": 31,
						"name": "【毛蟹炒毛豆组合】鲜活六月黄大闸蟹2只+带壳毛豆 400g",
						"price": "35.80",
						"vip_price": "0.00",
						"propaganda":"http://img.nodebook.top/2020_02_27_04_28_105536image/jpeg"
					},
					{
						"id": 32,
						"name": "加费尔德冷冻青虾仁 250g",
						"price": "28.80",
						"vip_price": "0.00",
						"propaganda":"http://img.nodebook.top/2020_02_27_04_28_105536image/jpeg"
					},
					{
						"id": 40,
						"name": "粮全其美葱香味手抓饼 900g/袋",
						"price": "20.80",
						"vip_price": "0.00",
						"propaganda":"http://img.nodebook.top/2020_02_27_04_28_105536image/jpeg"
					},
					{
						"id": 51,
						"name": "凡谷1号番茄 500g",
						"price": "7.90",
						"vip_price": "0.00",
						"propaganda":"http://img.nodebook.top/2020_02_27_04_28_105536image/jpeg"
					},
					{
						"id": 52,
						"name": "黄天鹅可生食鲜鸡蛋20枚 1kg",
						"price": "46.80",
						"vip_price": "0.00",
						"propaganda":"http://img.nodebook.top/2020_02_27_04_28_105536image/jpeg"
					},
					{
						"id": 56,
						"name": "粮管家乳玉香米 5kg/袋",
						"price": "44.80",
						"vip_price": "0.00",
						"propaganda":"http://img.nodebook.top/2020_02_27_04_28_105536image/jpeg"
					},
					{
						"id": 75,
						"name": "卫龙香辣味大面筋 65g/袋",
						"price": "998.00",
						"vip_price": "0.00",
						"propaganda":"http://img.nodebook.top/2020_02_27_04_28_105536image/jpeg"
					}
				],
			cuIconList: [{
					cuIcon: 'cardboardfill',
					color: 'red',
					badge: 120,
					name: 'VR'
				}, {
					cuIcon: 'recordfill',
					color: 'orange',
					badge: 1,
					name: '录像'
				}, {
					cuIcon: 'picfill',
					color: 'yellow',
					badge: 0,
					name: '图像'
				}, {
					cuIcon: 'noticefill',
					color: 'olive',
					badge: 22,
					name: '通知'
				}, {
					cuIcon: 'upstagefill',
					color: 'cyan',
					badge: 0,
					name: '排行榜'
				}, {
					cuIcon: 'clothesfill',
					color: 'blue',
					badge: 0,
					name: '皮肤'
				}, {
					cuIcon: 'discoverfill',
					color: 'purple',
					badge: 0,
					name: '发现'
				}, {
					cuIcon: 'questionfill',
					color: 'mauve',
					badge: 0,
					name: '帮助'
				}, {
					cuIcon: 'commandfill',
					color: 'purple',
					badge: 0,
					name: '问答'
				}, {
					cuIcon: 'brandfill',
					color: 'mauve',
					badge: 0,
					name: '版权'
				}],
				cardCur: 0,
				swiperList: [{
					id: 0,
					type: 'image',
					url: 'http://img.nodebook.top/2020_02_27_06_23_4833913image/jpeg'
				}, {
					id: 1,
					type: 'image',
					url: 'http://img.nodebook.top/2020_02_27_06_23_4833913image/jpeg',
				}, {
					id: 2,
					type: 'image',
					url: 'http://img.nodebook.top/2020_02_27_06_23_4833913image/jpeg'
				}],
				dotStyle: false,
				towerStart: 0,
				direction: ''
		};
	},
	onLoad() {

		},
		methods: {

		}
	}
</script>

<style scoped>
	.content {
		width: 100%;
		height: 100%;
		background: #FFFFFF;
	}

	.status_bar {
		height: var(--status-bar-height);
		width: 100%;
		background-image: linear-gradient(left top, #6C37B4, #E4038E);
		color: #FFFFFF;
	}

	.contentBox {
		width: 100%;
		height: calc(100% - var(--status-bar-height));
		position: relative;
		overflow: hidden;
	}

	/* 滚动区域 */
	.scroll-Y {
		width: 100%;
		height: calc(100% - var(--status-bar-height));
		overflow: hidden;
		z-index: 10;
	}

	/* 轮播图 */
	.screen-swiper {
		height: 416rpx !important;
	}

	.screen-swiper {
		height: 416rpx !important;
	}

	/* 导航 */
	.Index-Nav {
		width: 100%;
		height: 380rpx;
		padding-bottom: 20rpx;
		box-sizing: border-box;
		display: flex;
		justify-content: space-between;
		flex-flow: wrap;
	}

	.Index-Nav-List {
		width: 110rpx;
		height: 180rpx;
		padding-top: 20rpx;
		display: flex;
		justify-content: center;
		flex-flow: wrap;
		margin: 0 20rpx;
	}

	.Index-Nav-List image {
		width: 100rpx;
		height: 100rpx;
		border-radius: 50rpx;
		overflow: hidden;
	}

	.Index-Nav-List-Text {
		width: 100%;
		height: 58rpx;
		line-height: 58rpx;
		font-size: 24rpx;
		/* font-weight: 600; */
		color: #3C3B3B;
		overflow: hidden;
		text-align: center;
	}

	/* 会员卡 */
	.Index-vip {
		width: 100%;
		height: 126rpx;
		background: #F8F4F5;
		padding: 20rpx;
		box-sizing: border-box;
		box-sizing: border-box;
	}

	.Index-vip-list {
		width: 100%;
		height: 100%;
		background-image: linear-gradient(left top, #3DB762, #44CE61);
		border-radius: 10rpx;
		display: flex;
		justify-content: space-between;
		font-size: 24rpx;
		color: #FFFFFF;
		line-height: 86rpx;
	}

	.Index-vip-list-icon {
		width: 86rpx;
		height: 100%;
		line-height: 86rpx;
		font-size: 40rpx;
		text-align: center;
		color: #F9E974;
	}

	.Index-vip-list-icon text {
		color: #F9E974;
	}

	.Index-vip-list-text {
		width: 450rpx;
		height: 100%;
	}

	.Index-vip-list-right {
		width: 150rpx;
		height: 100%;
	}

	/* 今日疯抢 */
	.Index-Rush {
		width: 100%;
		height: 102rpx;
		padding: 24rpx 20rpx 24rpx 15rpx;
		box-sizing: border-box;
		display: flex;
	}

	.Index-Rush-left {
		flex: 1;
		line-height: 54rpx;
		font-size: 36rpx;
		letter-spacing: 3rpx;
		font-weight: 700;
		display: flex;

	}

	.Index-Rush-right {
		width: 100rpx;
		height: 100%;
		line-height: 34rpx;
		font-size: 26rpx;
		color: #5BB384;
		font-weight: 600;
	}

	/* 今日疯抢 滚动图 */
	.scroll-view_H {
		height: 356rpx;
		width: 100%;
	}

	/* 要根据返回数量的多少调整盒子宽度 */
	.scroll-view-H-Box {
		height: 356rpx;
		width: 1320rpx;
		/* width: auto; */
		display: flex;
		justify-content: flex-start;

	}

	.scroll-view-item_H {
		width: 220rpx;
		height: 356rpx;
		/* float: left; */

	}

	/* .scroll-view-item_H:nth-child(1){
		background: #1CBBB4;
	} */
	.scroll-view-item_H-img {
		width: 220rpx;
		height: 190rpx;
		padding: 10rpx 20rpx 20rpx 20rpx;
		box-sizing: border-box;
	}

	.scroll-view-item_H-img image {
		width: 100%;
		height: 100%;
	}

	.scroll-view-item_H-name {
		width: 100%;
		height: 64rpx;
		line-height: 32rpx;
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-line-clamp: 2;
		-webkit-box-orient: vertic;
		padding: 0 20rpx;
		box-sizing: border-box;
		font-size: 24rpx;
		color: #101010;
	}

	.scroll-view-item_H-news {
		width: 100%;
		height: 106rpx;
		display: flex;
		justify-content: space-between;
	}

	.scroll-view-item_H-news-left {
		width: 130rpx;
		height: 100%;
		padding-top: 20rpx;
		box-sizing: border-box;
	}

	.scroll-view-item_H-news-left-top {
		width: 100%;
		height: 38rpx;
		line-height: 38rpx;
		color: #F15C6B;
		font-size: 28rpx;
		text-align: center;
	}

	.scroll-view-item_H-news-left-bottom {
		width: 100%;
		height: 26rpx;
		line-height: 26rpx;
		color: #A8A8A8;
		font-size: 17rpx;
		text-align: center;
		text-decoration: line-through;
	}

	.scroll-view-item_H-news-right {
		width: 82rpx;
		height: 100%;
		text-align: center;
		padding: 10rpx;
		box-sizing: border-box;
	}

	.scroll-view-item_H-news-right text {
		width: 60rpx;
		height: 60rpx;
		background: #3BB86A;
		border-radius: 30rpx;
		display: inline-block;
		line-height: 60rpx;
		font-size: 30rpx;
		color: #FFFFFF;
	}

	/* 横条 */
	.Index-Hr {
		width: 100%;
		height: 20rpx;
		background: #F8F4F5;
	}

	/* 猜你喜欢 */
	.Index-live {
		width: 100%;
		padding: 0 18rpx 18rpx;
		box-sizing: border-box;
		display: flex;
		justify-content: space-between;
		flex-flow: wrap;
	}

	.Index-live-list {
		width: 350rpx;
		height: 550rpx;
		box-shadow: 0 0 5rpx #EEEEEE;
		border: 1px solid #EEEEEE;
		border-radius: 10rpx;
		padding: 0rpx 20rpx 0rpx 20rpx;
		box-sizing: border-box;
		margin-bottom: 20rpx;
	}

	.Index-live-list-img {
		width: 100%;
		height: 340rpx;
		padding: 40rpx 5rpx;
		box-sizing: border-box;
	}

	.Index-live-list-img image {
		width: 100%;
		height: 100%;
	}

	.Index-live-list-text {
		width: 100%;
		height: 70rpx;
		line-height: 35rpx;
		color: #101010;
		font-size: 25rpx;
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-line-clamp: 2;
		-webkit-box-orient: vertic;
	}

	.Index-live-list-news {
		width: 100%;
		height: 136rpx;
		display: flex;
		justify-content: space-between;
	}

	.Index-live-list-news-left {
		width: 230rpx;
		height: 100%;
		overflow: hidden;
		/* display: flex;
		flex-direction:column;
		justify-content:flex-start;
		align-items:center;
		flex-flow: wrap; */
		padding-top: 40rpx;
		box-sizing: border-box;
		/* display: flex;
		align-items: center;
		flex-flow: wrap; */
	}

	.Index-live-list-news-left-pick {
		width: 100%;
		height: 38rpx;
		color: #F45A6C;
		font-size: 27rpx;
		font-weight: 600;
		line-height: 38rpx;

	}

	.Index-live-list-news-left-vip {
		width: 100%;
		height: 40rpx;
		color: #30BD4C;
		font-size: 22rpx;
		line-height: 40rpx;


	}

	.Index-live-list-news-left-vip text {
		background: #30BD4C;
		color: #FFFFFF;
		font-size: 16rpx;
		padding: 5rpx 10rpx;
		margin-left: 10rpx;
	}

	.Index-live-list-news-right {
		width: 78rpx;
		height: 100%;
		overflow: hidden;
		padding-top: 40rpx;
		box-sizing: border-box;
	}

	.Index-live-list-news-right text {
		width: 60rpx;
		height: 60rpx;
		display: inline-block;
		background: #47C470;
		border-radius: 30rpx;
		text-align: center;
		line-height: 60rpx;
		color: #FFFFFF;
		font-size: 30rpx;
	}

	.shoping-buy-right {
		width: 270rpx;
		height: 54rpx;
		/* 		background: #FEEFE8; */
		color: #F1627D;
		text-align: center;
		line-height: 88rpx;
		font-size: 22rpx;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.shoping-buy-right-time {
		display: inline-block;
		width: 38rpx;
		height: 30rpx;
		background: #FD6069;
		color: #FFFFFF;
		font-size: 16rpx;
		line-height: 30rpx;
		text-align: center;
		border-radius: 5rpx;
		margin: 0 10rpx;

	}
</style>
