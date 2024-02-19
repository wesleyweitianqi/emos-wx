<template>
	<view>
		<h1>Hello</h1>
		<view>{{username}}</view>
		<view v-for="one in tel">{{one}}</view>
		<view v-if="age >=18">{{age}}
			<button @tap="signup()">sign up</button>
		</view>
		<input type="text" v-model="address" placeholder="input address"/>
		<view>{{address}}</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				username: "Welsey",
				tel: ['1235649955','14513342531'],
				age: 30,
				address:""
			}
		},
		methods: {
			sighup: function(){
				uni.showToast({
					title: "sign up clicked"
				})
			}
		}
	}
</script>

<style>

</style>
