<template>
	<view class="content">
		<view class="top-content">
			<uni-icons class="menu" type="list" size="30" @click="showDrawer('showLeft')"></uni-icons>
			<text class="storeName">徐州核心库</text>
		</view>
		<!-- 设置 -->
		<uni-drawer ref="showLeft" mode="left" :width="320" @change="change($event, 'showLeft')">
			<view class="menu-content">
				<view class="info">
					<view class="user-info">
						<view class="user-image"></view>
						<view class="user-name">项羽-门店经理</view>
					</view>
					<view class="app-infos">
						<text>仓库管理</text>
						<text>1.0.2.0</text>
					</view>
				</view>

				<view class="settingItem">
					<text>所属组织</text>
					<view><text class="setting-tips">徐州配送公司</text></view>
				</view>
				<view class="settingItem">
					<text>切换仓库</text>
					<text class="setting-tips">徐州核心库</text>
					<view class="setting-tips"><uni-icons type="right" size="20"></uni-icons></view>
				</view>
				<view class="settingItem">
					<text>扫描声音</text>
					<view class="setting-tips">
						<text>设置</text>
						<uni-icons type="right" size="20"></uni-icons>
					</view>
				</view>
				<view class="settingItem">
					<text>相关参数</text>
					<view class="setting-tips">
						<text>设置</text>
						<uni-icons type="right" size="20"></uni-icons>
					</view>
				</view>
				<view class="settingItem">
					<text>打印设置</text>
					<view class="setting-tips">
						<text>设置</text>
						<uni-icons type="right" size="20"></uni-icons>
					</view>
				</view>
				<view class="settingItem">
					<text>检查更新</text>
					<view class="setting-tips">
						<text style="color: red!important;">有新版本</text>
						<uni-icons type="right" size="20"></uni-icons>
					</view>
				</view>
				<!-- <button @click="closeDrawer('showLeft')"><text class="word-btn-white">返回</text></button> -->
				<view class="logout">
					<view class="logoutBlock"><button class="logoutBtn" @click="logout">退出登录</button></view>
				</view>
			</view>
		</uni-drawer>
		<!-- 菜单 -->
		<!-- 收货入库 -->
		<view class="menu-block">
			<view class="menu-title">
				<view style="width: 5px;background-color: red;height: 100%;"></view>
				<text>收货入库</text>
			</view>
			<view class="menu-list">
				<view class="menu-item" @click="toPage('putaway')">
					<i class="iconfont icon-ruku menu-icon icon-red"></i>
					<text class="menu-name">入库上架</text>
				</view>
				<view class="menu-item">
					<i class="iconfont icon-icon-receive menu-icon icon-blue"></i>
					<text class="menu-name">收货确认</text>
				</view>
				<view class="menu-item">
					<i class="iconfont icon-rukusaomiao menu-icon" style="color: #5ca75c!important;;"></i>
					<text class="menu-name">入库扫描</text>
				</view>
			</view>
		</view>
		<!-- 在库管理 -->
		<view class="menu-block">
			<view class="menu-title">
				<view style="width: 5px;background-color: red;height: 100%;"></view>
				<text>在库管理</text>
			</view>
			<view class="menu-list">
				<view class="menu-item">
					<i class="iconfont icon-tuanduicankaoxian- menu-icon icon-blue"></i>
					<text class="menu-name">库存转单</text>
				</view>
				<view class="menu-item">
					<i class="iconfont icon-tuanduicankaoxian- menu-icon icon-blue"></i>
					<text class="menu-name">理货</text>
				</view>
				<view class="menu-item">
					<i class="iconfont icon-kucunchaxun menu-icon icon-green"></i>
					<text class="menu-name">在库查询</text>
				</view>
			</view>
		</view>
		<!-- 出库管理 -->
		<view class="menu-block">
			<view class="menu-title">
				<view style="width: 5px;background-color: red;height: 100%;"></view>
				<text>出库管理</text>
			</view>
			<view class="menu-list">
				<view class="menu-item">
					<i class="iconfont icon-chuku menu-icon icon-orange"></i>
					<text class="menu-name">出库扫描</text>
				</view>
				<view class="menu-item">
					<i class="iconfont icon-peijianchukutongji menu-icon icon-orange"></i>
					<text class="menu-name">备货出库</text>
				</view>
				<view class="menu-item">
					<i class="iconfont icon-icon-svg-02 menu-icon icon-blue"></i>
					<text class="menu-name">装车扫描</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			title: 'Hello12222333'

		};
	},
	onLoad() {},
	methods: {
		showDrawer(e) {
			this.$refs[e].open();
		},
		// 关闭窗口
		closeDrawer(e) {
			this.$refs[e].close();
		},
		// 抽屉状态发生变化触发
		change(e, type) {
			console.log((type === 'showLeft' ? '左窗口' : '右窗口') + (e ? '打开' : '关闭'));
			this[type] = e;
		},
		logout() {
			uni.navigateTo({
				url: '/pages/login/login'
			});
		},
		toPage(pageName) {
			let pageUrl = `/pages/${pageName}/${pageName}`;
			let data = { index: 1, num: 9 };
			uni.navigateTo({
				url: pageUrl,
				events:data
			});
		}
	}
};
</script>

<style lang="scss" scoped>
.content {
	width: 100vw;
	height: 100vh;
	display: flex;
	flex-direction: column;
	background-color: #f6f1f1;

	.top-content {
		width: 100%;
		height: 100px;
		padding: 10px 0;
		background-color: white;
		display: flex;
		align-items: flex-end;

		.storeName {
			width: 100%;
			display: flex;
			justify-content: center;
			font-size: 26px;
		}

		.menu {
			margin-left: 25px;
		}
	}
	.menu-content {
		width: 100%;
		height: 100vh;
		position: relative;
		display: flex;
		flex-direction: column;
		background-color: #f6f1f1;
		.info {
			width: 100%;
			height: 180px;
			display: flex;
			align-items: flex-end;
			justify-content: space-between;
			background-color: #ee611b;
			.user-info {
				height: 75%;
				display: flex;
				flex-direction: column;
				padding: 20px;

				.user-image {
					height: 70%;
				}
				.user-name {
					font-size: 20px;
					color: white;
				}
			}
			.app-infos {
				width: 40%;
				height: 75%;
				padding: 20px;
				display: flex;
				flex-direction: column;
				align-items: flex-end;
				text {
					font-size: 20px;
					margin: 2px 0;
					color: white;
				}
			}
		}

		.settingItem {
			width: 100%;
			height: 60px;
			padding: 0 20px;
			margin-bottom: 10px;
			background-color: white;
			display: flex;
			justify-content: space-between;
			align-items: center;
			/deep/.setting-tips,
			.setting-tips text,
			.setting-tips .uni-icons {
				color: #a5adad !important;
			}
		}

		.logout {
			width: 100%;
			height: 100%;
			// position: absolute;
			flex: 1;
			.logoutBlock {
				width: 100%;
				height: 100%;
				display: flex;
				align-items: flex-end;
			}
			.logoutBtn {
				width: 80%;
				margin-bottom: 30px;
				color: white;
				background-color: red;
			}
		}
	}
}

.menu-block {
	width: 100%;
	padding: 20px;
	display: flex;
	flex-direction: column;
	background-color: white;
	margin: 10px 0;
	.menu-title {
		height: 20px;
		display: flex;
		align-items: center;
		margin-bottom: 25px;
		text {
			font-size: 20px;
			font-weight: bold;
			margin-left: 10px;
		}
	}
	.menu-list {
		width: 100%;
		display: flex;
		flex-wrap: wrap;
		.menu-item {
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
			margin: 10px 12px;
			.menu-icon {
				font-size: 60px;
				color: #f8eeee !important;
				// background-color: red;
				border-radius: 10px;
			}
			.icon-red {
				background-color: red;
			}
			.icon-green {
				background-color: #5ca75c;
			}
			.icon-blue {
				background-color: dodgerblue;
			}
			.icon-orange {
				background-color: orange;
			}
			.menu-name {
				margin-top: 15px;
			}
		}
	}
}
text {
	font-size: 18px;
}
</style>

<style></style>
