<template>
	<view class="login-container">
		<text class="appTitle">仓库管理</text>
		<view class="login-body">
			<view class="userItem">
				<uni-easyinput :inputBorder='false' placeholderStyle="font-size:18px" prefixIcon="person" v-model="username" placeholder="用户名"></uni-easyinput>
			</view>
			<view class="userItem">
				<uni-easyinput :inputBorder='false' placeholderStyle="font-size:18px" prefixIcon="locked" :clearable='true' type="password" v-model="password" placeholder="密码"></uni-easyinput>
			</view>
		</view>
		<view class="userItem userOption">
			<text>默认记忆密码</text>
			<switch checked="true" @change="changeSavePwd" color="red" style="margin-left: 10px;" />
		</view>
		<view class="loginBtn">
			<button @click="toIndex">登录</button>
		</view>
		<view class="serverOption">
			<text>服务器地址变动</text>
			<text class="changeServer" @click="toSetting">服务器设置</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				username: '',
				password: '',
				savePwd: false
			};
		},
		methods:{
			changeSavePwd(e){
				// console.log(e)
			},
			toSetting(){
				uni.navigateTo({
					url:"/pages/serverSetting/serverSetting"
				})
			},
			toIndex(){
				uni.navigateTo({
					url:"/pages/index/index"
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	
	.login-container {
		width: 100vw;
		// height: 100vh;
		padding: 70px;
		display: flex;
		flex-direction: column;

		.appTitle {
			height: 25vh;
			display: flex;
			justify-content: center;
			align-items: center;
			font-size: 36px;
		}
		.userItem{
			display: flex;
			align-items: center;
			height: 70px;
			border-bottom: 1px solid #d4d4d4;
			/deep/ input{
				padding-left: 10px;
				font-size: 18px;
			}
			/deep/.uni-icons{
				font-size: 26px !important;
				font-weight: bold;
				color: #a6a6a6 !important;
			}
		}
		.userOption{
			display: flex;
			justify-content: space-between;
		}
		.loginBtn{
			margin-top: 60px;
			button{
				background-color: red;
				color: white;
			}
		}
		.serverOption{
			display: flex;
			justify-content: center;
			margin-top: 30px;
			.changeServer{
				color: red;
				margin-left: 5px;
			}
		}
	}
	text{
		font-size: 18px;
	}
</style>
