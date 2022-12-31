<template>
	<div class="header-todo">
		<div class="input-box">
			<input @keyup.enter="enterInput" v-model="val" class="enter-input"  placeholder="请输入你的任务名称,按回车键确认" type="text">
		</div>	  
	</div>	
</template>

<script>
import Bus from '../../bus.js'
	export default{
		name:"TodoHeader",
		data(){
			return {
				val:""
			}
		},
		methods:{
			enterInput(){
				//获取所有缓存
				//将新的内容添加在缓存中去
				//在设置到缓存中去
				let listArr = JSON.parse(window.localStorage.getItem('listTodo')) || [];
				listArr.unshift({"title":this.val,checked:false,"isShow":true})
				window.localStorage.setItem('listTodo',JSON.stringify(listArr))
				Bus.$emit('onEvent');
				this.val = ''
			}
		}
	}
	
	
</script>

<style>
	.header-todo{
		width: 100%;
		
	}
	.enter-input{
		box-sizing: border-box;
		width: 100%;
		height: 40px; 
		line-height: 40px; 
		padding-left: 12px;
		font-size:16px;
		border-radius: 10px;
		border: none;
		outline:none;
	}
	input::-webkit-input-placeholder{
		font-size: 14px;
	}
</style>