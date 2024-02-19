<template>
	<view>
		<image src="../../static/logo-2.png" mode="widthFix" class="logo"></image>
		<view class="register-container">
			<input type="text" placeholder="input invitation number" class="register-code" maxlength="6" v-model="registerCode" />
			<view class="register-desc">After created, you will receive invitation code from email</view>
			<button class="register-btn" open-type="getUserInfo" @tap="register()">Register</button>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			registerCode:""
		};
	},
	methods: {
		register: function() {
			let that=this
			if(that.registerCode==null||that.registerCode.length==0){
				uni.showToast({
					icon:"none",
					title:"invitation cannot be null"
				})
				return
			}
			else if(/^[0-9]{6}$/.test(that.registerCode)==false){
				uni.showToast({
					icon:"none",
					title:"invitaion length should be 6 digits"
				})
				return
			}
			uni.login({
				provider: 'weixin',
				success: function(resp) {
					console.log(resp.code)
					let code = resp.code;
					uni.getUserInfo({
						provider: 'weixin',
						success: function(resp) {
							let nickName = resp.userInfo.nickName;
							let avatarUrl = resp.userInfo.avatarUrl;
							// console.log(nickName);
							// console.log(avatarUrl);
							let data={
								code:code,
								nickname:nickName,
								photo:avatarUrl,
								registerCode:that.registerCode
							}
							that.ajax(that.url.register,"POST",data,function(resp){
								let permission=resp.data.permission
								uni.setStorageSync("permission",permission)
								console.log(permission)
								//跳转到index页面
								uni.switchTab({
									url:"../index/index"
								})
							})
						}
					});
				}
			});
		}
	}
};
</script>

<style lang="less">
@import url('register.less');
</style>
