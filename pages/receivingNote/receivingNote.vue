<template>
	<view class="container">
		<view class="search-content">
			<uni-easyinput class="uni-mt-5 searchbox" suffixIcon="scan" v-model="keyword" placeholder="请扫描或输入收货单"
				@iconClick="scanCode"></uni-easyinput>
			</uni-section>
		</view>
		<view class="note-list">
			<view class="note-item" v-for="(n, index) in notelist" :key="index">
				<view class="note-icon-view">
					<uni-icons class="note-icon" type="bars" size="30"></uni-icons>
				</view>
				<view class="note-info">
					<text class="note-num">{{n.noteid}}</text>
					<text class="gray">{{n.noteTime}} {{n.noteState}}</text>
					<text class="gray">收货人：{{n.notePerson}}  &nbsp;&nbsp; 分包数：{{n.noteSubNum}}</text>
				</view>
				<label>
					<checkbox :value="n.noteid" color="red" />
				</label>
			</view>
		</view>
		<view class="loaded" v-if="isloaded">
			<text>~总要有个尽头吧~</text>
		</view>
		<view class="confirm-content">
			<button>确认</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				keyword: "",
				notelist: [{
						noteid: "FC20230217042333",
						noteTime: "2023-02-17 16:23:33",
						noteState: "收货",
						noteSubNum: "2",
						notePerson: "项羽",
						isCheck: false
					},
					{
						noteid: "FC20230217042333",
						noteTime: "2023-02-17 16:23:33",
						noteState: "收货",
						noteSubNum: "2",
						notePerson: "项羽",
						isCheck: false
					},
					{
						noteid: "FC20230217042333",
						noteTime: "2023-02-17 16:23:33",
						noteState: "收货",
						noteSubNum: "2",
						notePerson: "项羽",
						isCheck: false
					},
					{
						noteid: "FC20230217042333",
						noteTime: "2023-02-17 16:23:33",
						noteState: "收货",
						noteSubNum: "2",
						notePerson: "项羽",
						isCheck: false
					},
					{
						noteid: "FC20230217042333",
						noteTime: "2023-02-17 16:23:33",
						noteState: "收货",
						noteSubNum: "2",
						notePerson: "项羽",
						isCheck: false
					},
					{
						noteid: "FC20230217042333",
						noteTime: "2023-02-17 16:23:33",
						noteState: "收货",
						noteSubNum: "2",
						notePerson: "项羽",
						isCheck: false
					},
					{
						noteid: "FC20230217042333",
						noteTime: "2023-02-17 16:23:33",
						noteState: "收货",
						noteSubNum: "2",
						notePerson: "项羽",
						isCheck: false
					},
					{
						noteid: "FC20230217042333",
						noteTime: "2023-02-17 16:23:33",
						noteState: "收货",
						noteSubNum: "2",
						notePerson: "项羽",
						isCheck: false
					},
					{
						noteid: "FC20230217042333",
						noteTime: "2023-02-17 16:23:33",
						noteState: "收货",
						noteSubNum: "2",
						notePerson: "项羽",
						isCheck: false
					},
					{
						noteid: "FC20230217042333",
						noteTime: "2023-02-17 16:23:33",
						noteState: "收货",
						noteSubNum: "2",
						notePerson: "项羽",
						isCheck: false
					},
					{
						noteid: "FC20230217042333",
						noteTime: "2023-02-17 16:23:33",
						noteState: "收货",
						noteSubNum: "2",
						notePerson: "项羽",
						isCheck: false
					},
					{
						noteid: "FC20230217042333",
						noteTime: "2023-02-17 16:23:33",
						noteState: "收货",
						noteSubNum: "2",
						notePerson: "项羽",
						isCheck: false
					}
				],
				isloaded: true
			};
		},
		onPullDownRefresh(){
			console.log("下拉刷新")
			let timer = setTimeout(()=>{
				uni.stopPullDownRefresh();
			}, 1500)
		},
		methods: {
			scanCode() {
				let that = this;
				uni.scanCode({
					success: function(res) {
						console.log('条码类型：' + res.scanType);
						console.log('条码内容：' + res.result);
						that.result = res.result
					}
				});
			}
		}
	}
</script>

<style lang="scss" scoped>
	.container {
		width: 100vw;
		height: 100%;
		display: flex;
		flex-direction: column;
		background-color: #f6f1f1;

		.search-content {
			width: 100%;
			padding: 20px;
			position: sticky;
			background-color: white;
			top: var(--window-top);
			z-index: 9999;
		}

		.note-list {
			width: 100%;
			display: flex;
			flex-wrap: wrap;
			background-color: #f6f1f1;

			.note-item {
				width: 100%;
				display: flex;
				align-items: center;
				background-color: white;
				margin-top: 20px;
				padding: 20px;
				border-radius: 20px;

				.note-icon-view {
					display: flex;
					align-items: center;
					justify-content: center;
					width: 50px;
					height: 50px;
					border-radius: 50% !important;
					background-color: #eabeb3;

					.note-icon {
						margin: 0 !important;
						color: white !important;
					}
				}

				.note-info {
					display: flex;
					flex: 1;
					flex-direction: column;
					margin-left: 20px;
					
					.note-num{
						font-size: 20px;
						font-weight: 900;
					}
					text{
						padding: 3px;
					}
				}
				
				
			}
		}
		
		.loaded{
			width: 100%;
			display: flex;
			justify-content: center;
			background-color: #f6f1f1;
			padding: 20px;
		}
		.confirm-content{
			width: 100%;
			display: flex;
			position: sticky;
			bottom: var(--window-bottom);
			padding: 10px;
			background-color: white;
			button{
				width: 80%;
				border-radius: 30px;
				color: white;
				background-color: red;
			}
		}
	}

	/deep/.is-input-border {
		border-radius: 20px !important;
	}

	/deep/.uni-icons {
		margin-right: 10px;
		color: red !important;
	}
	
	/deep/.uni-checkbox-input{
		border-radius: 50%;
	}
</style>
