<template>
	<view class="content">
		<view class="top-content">
			<!-- 自定义导航栏 -->
			<view class="nav-content">
				<uni-nav-bar class="nav-bar" :border='false' color="white" backgroundColor="red" rightWidth="80px"
					leftWidth="80px" @clickLeft="goBack" @clickRight="toReceivingNote">
					<view slot="left" class="rm">
						<uni-icons type="left" size="20" style="color: white;"></uni-icons>
						<text style="font-size: 16px;">返回</text>
					</view>
					<view class="bar-title">
						<text>徐州核心库-入库上架</text>
					</view>
					<view slot="right" class="rm">
						<text style="font-size: 16px;">收货单</text>
						<uni-icons type="right" size="20" style="color: white;"></uni-icons>
					</view>
				</uni-nav-bar>
			</view>
			<!-- 搜索 -->
			<view class="search-content">
				<uni-easyinput class="uni-mt-5 searchbox" suffixIcon="scan" v-model="keyword"
					placeholder="请扫描包装条码或输入提货码" @iconClick="scanCode"></uni-easyinput>
				</uni-section>
				<view class="search-option">
					<view class="search-item" @click="cureentSearchType = 1">
						<text class="search-name">扫描</text>
						<view v-if="cureentSearchType == 1" class="cureent-search-type"></view>
					</view>
					<view class="search-item" @click="cureentSearchType = 2">
						<text class="search-name">明细</text>
						<view v-if="cureentSearchType == 2" class="cureent-search-type"></view>
					</view>
					<view class="search-item" @click="cureentSearchType = 3">
						<text class="search-name">扫描日志</text>
						<view v-if="cureentSearchType == 3" class="cureent-search-type"></view>
					</view>
				</view>
			</view>
		</view>
		<!-- 扫描列表 -->
		<view class="scanlist" v-if="cureentSearchType == 1">
			<view class="">本次：1.05</view>
			<view class="">暂存：1.05</view>
			<view class="" style="color: deepskyblue;">入库看板<uni-icons type="right" style="color: deepskyblue;"></uni-icons></view>
		</view>
		<!-- 提示窗示例 -->
		<uni-popup ref="alertDialog" type="dialog">
			<uni-popup-dialog  cancelText="关闭" confirmText="同意" title="通知" :content="v" @confirm="dialogConfirm"
				@close="dialogClose"></uni-popup-dialog>
		</uni-popup>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				keyword: "",
				cureentSearchType: 1,
				result: "",
				v: ''
			};
		},
		onLoad(option){
			console.log("onload-data", option)
		},

		mounted(){
			this.getAppInfo()
			this.type = "info"
			this.$refs.alertDialog.open()
		},
		methods: {
			goBack() {
				uni.navigateBack();
			},
			toReceivingNote() {
				uni.navigateTo({
					url: "/pages/receivingNote/receivingNote"
				})
			},
			scanCode() {
				let that = this;
				uni.scanCode({
					success: function(res) {
						console.log('条码类型：' + res.scanType);
						console.log('条码内容：' + res.result);
						that.result = res.result
					}
				});
			},
			dialogConfirm(){},
			dialogClose(){},
			
			getAppInfo() {
				let that = this
				// #ifdef APP-PLUS
					plus.runtime.getProperty( plus.runtime.appid, function ( wgtinfo ) {
						that.v = wgtinfo.version
					} );
				// #endif

				
			}
			
		}
	}
</script>

<style lang="scss" scoped>
	.content {
		width: 100vw;
		height: 100vh;
		background-color: #f6f1f1;

	}

	.top-content {
		width: 100vw;
		background-color: red;
	}

	.nav-content {
		width: 100%;
		height: 90px;
		display: flex;
		align-items: flex-end;

		.nav-bar {
			width: 100%;
		}

		.bar-title {
			width: 100%;
			display: flex;
			justify-content: center;
			align-items: center;
			font-size: 18px;
		}

		.rm {
			height: 100%;
			display: flex;
			align-items: center;
		}
	}

	.search-content {
		width: 100%;
		height: 100px;
		padding: 10px;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: space-between;

		.searchbox {

			// width: 80%;
			/deep/.is-input-border {
				border-radius: 20px !important;
			}

			/deep/.uni-icons {
				margin-right: 10px;
				color: red !important;
			}

		}

		.search-option {
			width: 100%;
			display: flex;
			justify-content: space-between;

			.search-item {
				height: 35px;
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: space-between;
				flex: 1;

				.search-name {
					color: white;
					font-size: 20px;
					font-weight: bold;
				}

				.cureent-search-type {
					width: 20px;
					height: 4px;
					background-color: white;
					border-radius: 2px;
				}
			}
		}
	}
	
	.scanlist{
		width: 100%;
		display: flex;
		justify-content: space-between;
		padding: 10px 20px;
		background-color: white;
	}
</style>
