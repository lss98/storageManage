<template>
	<view class="setting-container">
		<view class="settingBlock">
			<view class="settingTitle">
				<text>服务器设置：</text>
			</view>
			<view class="settingItme">
				<text>服务器</text>
				<uni-easyinput class="uni-mt-5" trim="all" v-model="serverUrl" placeholder="请输入服务器地址" @input="input"></uni-easyinput>
			</view>
			<view class="settingItme">
				<text>企业号</text>
				<uni-easyinput class="uni-mt-5" trim="all" v-model="serverUrl" placeholder="请输入企业服务号" @input="input"></uni-easyinput>
			</view>
		</view>
		<view class="settingBlock">
			<view class="settingTitle">
				<text>广播输出参数...：</text>
				<text class="reset">恢复出厂设置</text>
			</view>
			<view class="settingItme">
				<text>广播动作</text>
				<uni-easyinput class="uni-mt-5" trim="all" v-model="serverUrl" placeholder="请输入广播动作" @input="input"></uni-easyinput>
			</view>
			<view class="settingItme">
				<text>数据标签</text>
				<uni-easyinput class="uni-mt-5" trim="all" v-model="serverUrl" placeholder="请输入数据标签" @input="input"></uni-easyinput>
			</view>
		</view>
		<button class="nextBtn" @click="toLogin">下一步</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},methods:{
			toLogin(){
				uni.navigateTo({
					url:'/pages/login/login'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	
	.setting-container{
		width: 100vw;
		height: 100vh;
		padding: 30px;
		display: flex;
		flex-direction: column;
		
		.settingBlock{
			margin: 10px 0;
			.settingTitle{
				display: flex;
				justify-content: space-between;
				text{
					color: darkgrey;
				}
				.reset{
					color: red;
				}
			}
			.settingItme{
				width: 100%;
				display: flex;
				justify-content: space-between;
				align-items: center;
				
				text{
					font-size: 20px;
					margin: 15px 20px 15px 0;
				}
				
			}
		}
		
	}
	text{
		font-size: 20px;
	}
	
	.nextBtn{
		width: 80%;
		background-color: red;
		color: white;
		margin-top: 30px;
		display: flex;
		justify-content: center;
		
	}
	

</style>
