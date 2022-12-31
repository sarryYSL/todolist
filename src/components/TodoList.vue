<template>
	<div class="todo-item-box">
		<TodoItem></TodoItem>
	</div>
</template>
	
<script>
import TodoItem from './TodoItem.vue'
export default{
		name:"TodoList",
		data(){
			return {}
		},
		components:{
			TodoItem
		},
		created() {
			
		}
	}	
</script>

<style>
	.todo-item-box{
		width: 92%;
		border: 1px solid #eee;
		box-sizing: border-box;
		margin-top: 20px;
		padding: 20px;
	}
</style>