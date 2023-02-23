<script>
export default {
	onLaunch: function() {
		console.log('App Launch');
		// // #ifdef APP-PLUS
		// plus.runtime.getProperty(plus.runtime.appid, function(widgetInfo) {
		// 	console.log(widgetInfo);
		// 	uni.request({
		// 		url: 'http://192.168.72.219:8000/api/app/update',
		// 		data: {
		// 			version: widgetInfo.version,
		// 			name: widgetInfo.name
		// 		},
		// 		method: 'GET',
		// 		success: result => {
		// 			var data = result.data.result[0];
		// 			console.log(data);
		// 			let cv = widgetInfo.version
		// 			let nv = data.version
		// 			let cureentVersion = parseInt(cv.replace(/[.]/g, ''));
		// 			let newVersion = parseInt(nv.replace(/[.]/g, ''));
		// 			console.log(cureentVersion, newVersion)
		// 			let url = 'http://192.168.72.219:8000/static/appdata' + data.fileUrl
		// 			// let url = "http://192.168.72.219:8000/static/appdata/__UNI__7089363.wgt"
		// 			// let url = 'http://vacloud.mtstar.net/image/default/48E69AA6B8294030AE7CDE81748B88BE-6-2.jpeg'
		// 			console.log(url)
		// 			if (newVersion > cureentVersion && data.type == 1) {
		// 				console.log("888")
		// 				uni.downloadFile({
		// 					url: url,
		// 					success: downloadResult => {
		// 						console.log("dend",downloadResult);
		// 						if (downloadResult.statusCode === 200) {
		// 							plus.runtime.install(
		// 								downloadResult.tempFilePath,
		// 								{
		// 									force: false //是否校验版本 true不校验
		// 									// force: true
		// 								},
		// 								function() {
		// 									console.log('install success...');
		// 									plus.runtime.restart(); //热更新要重新启动才能生效

		// 								},
		// 								function(e) {
		// 									console.error('install fail...', e);
		// 								}
		// 							);
		// 						}
		// 					},
		// 					complete: res =>{
		// 						console.log("999",res)
		// 					}
		// 				});
		// 			}
		// 		},
		// 		fail: e => {
		// 			console.log('err', e);
		// 		},
		// 		complete: res => {
		// 			console.log(res);
		// 		}
		// 	});
		// });
		// // #endif

		//#ifdef APP-PLUS
		var server = 'http://192.168.72.219:8000/api/app/update'; //检查更新地址

		plus.runtime.getProperty(plus.runtime.appid, function(wgtinfo) {
			var req = {
				//升级检测数据
				appid: wgtinfo.appid,
				version: wgtinfo.version
			};
			uni.request({
				url: server,
				data: req,
				success: res => {
					let cureentVersion = parseInt(req.version.replace(/[.]/g, ''));
					let newVersion = parseInt(res.data.result[0].version.replace(/[.]/g, ''));
					console.log(res.data);
					if (res.statusCode == 200 && res.data.result[0].type === 0 && newVersion > cureentVersion) {
						let appurl = 'http://192.168.72.219:8000/static/appdata' + res.data.result[0].fileUrl;
						uni.showModal({
							//提醒用户更新
							title: '更新提示',
							content: res.data.result[0].desc,
							success: res => {
								if (res.confirm) {
									// plus.runtime.openURL(appurl);
									uni.downloadFile({
										url: appurl,
										success: downloadResult => {
											console.log('dend', downloadResult);
											if (downloadResult.statusCode === 200) {
												plus.runtime.install(
													downloadResult.tempFilePath,
													{
														force: false //是否校验版本 true不校验
														// force: true
													},
													function() {
														console.log('install success...');
														plus.runtime.restart(); //热更新要重新启动才能生效
													},
													function(e) {
														console.error('install fail...', e);
													}
												);
											}
										},
										complete: res => {
											console.log('999', res);
										}
									});
								}
							}
						});
					}
				}
			});
		});

		//#endif
	},
	onShow: function() {
		console.log('App Show');
	},
	onHide: function() {
		console.log('App Hide');
	}
};
</script>

<style>
/*每个页面公共css */
@import './static/font_icon/storeManage/iconfont.css';
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}
</style>
