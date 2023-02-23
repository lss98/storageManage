<template>
	<view class="app-container">
		<view class="upload-content">
			<text>上传APP</text>
			<uni-file-picker
				class="selBtn"
				v-model="filelist"
				limit="1"
				file-mediatype="all"
				file-extname="apk,wgt"
				:auto-upload="false"
				@select="select"
				@progress="progress"
				@success="uploadSuccess"
			></uni-file-picker>
			<button class="uploadBtn">上传文件</button>
		</view>
		<view class="applist">
			<uni-table class="table-content" border stripe emptyText="暂无更多数据">
				<!-- 表头行 -->
				<uni-tr>
					<uni-th align="center">名称</uni-th>
					<uni-th align="center">版本</uni-th>
					<uni-th align="center">上传时间</uni-th>
					<uni-th align="center">类型</uni-th>
					<uni-th align="center">操作</uni-th>
				</uni-tr>
				<!-- 表格数据行 -->
				<uni-tr v-for="p in applist" :key="p.id">
					<uni-td>{{ p.name }}</uni-td>
					<uni-td>{{ p.version }}</uni-td>
					<uni-td>{{ p.uploadTime }}</uni-td>
					<uni-td>{{ p.type == '0' ? '整包更新(apk)' : '热更新(wgt)' }}</uni-td>
					<uni-td class="app-action">
						<button
							:class="{'isnewest': p.isnewest == '1'}"
							:disabled="p.isnewest == '1'"
							@click="newest(p.id)"
						>
							{{ p.isnewest == '1'? '当前最新版本' :'设置为最新版本'}}
						</button>
						<button @click="removeApp(p.id)" style="color: white; background-color: red;">删除</button>
					</uni-td>
				</uni-tr>
			</uni-table>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			filelist: [],
			applist: []
		};
	},
	mounted() {
		this.getapplist();
	},
	methods: {
		getapplist() {
			uni.request({
				url: '/api/get_app_list',
				method: 'GET',
				success: res => {
					console.log(res);
					this.applist = res.data.applist;
				}
			});
		},
		select(e) {
			console.log(e);
			let that = this
			let { name, extname, path } = e.tempFiles[0];
			let apptype = extname == 'apk'? 0 : 1
			console.log(name, extname, path);
			uni.uploadFile({
				url: '/api/upload_app',
				file: e.tempFiles[0].file,
				name: 'file',
				formData: {
					version: '1.0.0.3',
					uploadTime: '123',
					name: name,
					type: apptype
				},
				success: function(res) {
					console.log('上传结果', res);
					that.getapplist()
				}
			});
		},
		progress() {},
		uploadSuccess(e) {},
		newest(appid) {
			uni.request({
				url: '/api/change_newest_app',
				method: 'GET',
				data: {
					appid: appid,
				},
				success: res => {
					if (res.data.msg == 'ok') {
						this.getapplist();
					}
				}
			});
		},
		removeApp(appid){
			uni.request({
				url: '/api/delete_app',
				method: 'GET',
				data: {
					appid: appid,
				},
				success: res => {
					if (res.data.msg == 'ok') {
						this.getapplist();
					}
				}
			});
		}
	}
};
</script>

<style lang="scss" scoped>
.app-container {
	width: 100%;
	height: 100%;
	display: flex;
	flex-direction: column;
	padding: 50px 20px;

	.upload-content {
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: flex-end;

		.selBtn {
			text-align: right;
			padding: 10px 0;
			margin: 0;
			width: 300px;
		}

		.uploadBtn {
			margin: 0;
		}
	}
	.applist {
		width: 100%;
		display: flex;
		align-items: center;
		flex-direction: column;

		.table-content {
			width: 60%;
			.app-action {
				display: flex;
				justify-content: space-between;
			}

			.isnewest {
				color: white;
				background-color: lightgreen;
			}
		}
	}
}
</style>
