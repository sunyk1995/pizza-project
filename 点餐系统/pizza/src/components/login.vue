<template>
	<div id="login">
		<div class="row mt-3">
			<div class="col-md-12 col-lg-12">
				<div class="card text-center">
					<div class="card-body">
						<img class="mx-auto d-block" src="../assets/icon.png" />
						<form @submit.prevent='reset' class="mt-3">
							<div class="form-group">
								<label>邮箱</label>
								<input class='form-control'type="email" v-model='email' />
							</div>
							<div class="form-group">
								<label>密码</label>
								<input class='form-control'type="password" v-model='password' />
							</div>
							<button type="submit" class="btn btn-primary">登录</button>
						</form>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>
<script>
	import axios from 'axios'
	export default{
		name:'login',
		data(){
			return{
				email:'',
				password:'',
			}
		},
		beforeRouteEnter:(to,from,next)=>{
			next(vm=> vm.$store.commit('loginstatu',null))
		},
		methods:{
			reset(){
				axios.get('/posts.json').then((msg)=>{
					let data = msg.data;
					const dataArr = [];
					for(let attr in data){
						dataArr.push(data[attr])
					}
					const code = dataArr.filter(item=>{
						return item.email === this.email && item.password === this.password;
					})
					if(code != null && code.length){
						alert('登录成功')
						this.$store.commit('loginstatu',code[0].email)
						this.$router.push('/home')
						}
					else{
						alert('你输入的密码错误')
						this.$store.commit('loginstatu',null)
					}
				})
			}
		}
	}
</script>
<style>


</style>