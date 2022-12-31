<template>
	<div id="item">
		<div class="item" v-for="(item,index) in listTodo" :key='index'>
			<label class="label-title" :for="index">
				<div class="i-left">
					<input @change="selectItem(index)" :id="index" type="checkbox" :checked="item.checked">
					<div class="title">
						<span v-show="item.isShow">
							{{item.title}}
						</span>
						<input class="input-bd" ref="inputEdit" v-show="!item.isShow" @blur="changeEdit(index,$event)" type="text"
							v-model="item.title">
						</div>
				</div>
			</label>
			<div class="i-right">
				<img class="edit" v-show='item.isShow' @click="edit(index)" src="../assets/edit.png" alt="">
				<img class="del" v-show='item.isShow' @click="delList(index)" src="../assets/delete.png" alt="">
			</div>
		</div>
	</div>
</template>

<script>
	import Bus from '../../bus.js'
	export default {
		name: "TodoItem",
		data() {
			return {
				listTodo: JSON.parse(window.localStorage.getItem('listTodo')) || []
			}
		},
		watch: {
			'listTodo': {
				handler( value ) {
					window.localStorage.setItem('listTodo',JSON.stringify(value))
					Bus.$emit('itemLength', this.listTodo.length)
					let newArr = this.listTodo.filter((item) => {
						return item.checked == true
					})
					Bus.$emit('itemSelecet', newArr.length)
				},
				deep: true
			},
		},
		methods: {
			selectItem(index) {
				this.listTodo[index].checked = !this.listTodo[index].checked;
			},
			delList(index) {
				let isDel = confirm('确认要删除吗?');
				if (isDel == true) {
					this.listTodo.splice(index, 1)
				}
			},
			edit(index) {
				this.$nextTick(function() {
					this.$refs.inputEdit.focus();
				});

				this.listTodo[index].isShow = !this.listTodo[index].isShow
			},
			changeEdit(index, e) {
				this.listTodo[index].isShow = true;
				if (!e.target.value.trim()) return alert('内容不能为空')

			}
		},
		created() {
			// 拿到header传过来的最新值
			Bus.$on('onEvent', () => {
				this.listTodo = JSON.parse(window.localStorage.getItem('listTodo'));
			})
			// 清楚多个任务
			Bus.$on('delete', () => {
				this.listTodo = this.listTodo.filter((item) => {
					return item.checked == false
				})
			window.localStorage.setItem('listTodo',JSON.stringify(this.listTodo))
			})
			Bus.$on('selectAll', (msg) => {
				this.listTodo.forEach((item) => {
					if (msg == true) {
						item.checked = true;
					} else if (msg == false) {
						item.checked = false
					}

				})
			})
		}
	}
</script>

<style>
	.item {
		display: flex;
		justify-content: space-between;
		align-items: center;
		height: 40px;
		border-bottom: 1px solid #eee;
		padding: 0px 20px;
		
	}

	.item:hover {
		opacity: 1;
		background-color: #e3e3e3;
	}

	.item:hover .i-right {
		opacity: 1;
	}
	.label-title{
		width: 100%;
	}
	.title {
		cursor: pointer;
		text-overflow:ellipsis;
		white-space:nowrap;
		overflow:hidden;
	}

	.i-left {
		display: flex;
		align-items: center;
		width: 80%;
	}

	.i-right {
		display: flex;
		justify-content: center;
		opacity: 0;
		width: 20%;

	}

	.edit {
		width: 20px;
		height: 20px;
		cursor: pointer;
		margin-right: 20px;

	}

	.del {
		width: 20px;
		height: 20px;
		cursor: pointer;
	}
	.input-bd{
		outline: none;
		width:  auto;
	}
	input{
		outline: none; 
	} 
</style>
