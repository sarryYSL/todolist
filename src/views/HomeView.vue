<template>
  <div class="home">
		<div class="todo-box">
			<TodoHeader></TodoHeader>
			<TodoList></TodoList>
			<todoFooter></todoFooter>
		</div> 
  </div>
</template>

<script>
import TodoHeader from '@/components/TodoHeader.vue';
import TodoList from '@/components/TodoList.vue';
import todoFooter from '@/components/FooterTodo.vue';
export default {
  name: 'HomeView',
  components: {
	TodoHeader,
	TodoList,
	todoFooter
  }
}
</script>
<style>
	.todo-box{
		width: 92%;
		margin: 0 auto;
		padding: 20px;
		box-sizing:border-box;
		background-color: rgba(238, 238, 238, 0.5);
		border-radius: 20px;
	}
	
	
	
</style>
