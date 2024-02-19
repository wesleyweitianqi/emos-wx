<template>
	<view>
		<image src="../../static/logo-1.png" class="logo" mode="widthFix"></image>
		<view class="logo-title">EMOS online </view>
		<view class="logo-subtitle">Ver 2050.2</view>
		<button class="login-btn" open-type="getUserInfo" @tap="login()">Login</button>
		<view class="register-container">
			No account？
			<text class="register" @tap="toRegister()">Register</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			toRegister:function(){
				uni.navigateTo({
					url:"../register/register"
				})
			},
			login:function(){
				let that=this
				uni.login({
					provider:"weixin",
					success:function(resp){
						let code=resp.code
						console.log(code)
						that.ajax(that.url.login,"POST",{"code":code},function(resp){
							let permission=resp.data.permission
							uni.setStorageSync("permission",permission)
				
							uni.switchTab({
								url:"../index/index"
							})
							
						})
						
						
					},
					fail:function(e){
						uni.showToast({
							icon:"none",
							title:"execution exception"
						})
					}
				})
			}
		}
	}
</script>

<style lang="less">
	@import url("login.less");
</style>
