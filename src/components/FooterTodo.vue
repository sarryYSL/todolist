<template>
	<div class="footer">
		<div class="left">
			<label id="all">
			<input name="all" @change="selectAll" :checked="checked" type="checkbox">
			全选
			</label>
			<span>已完成 {{number.selectList}}/</span>
			<span>全部 {{ number.allLenght }} </span>
		</div>
		<div class="right">
			<img class="right-del" @click="delAll" src="../assets/all-del.png" alt="">
		</div>
	</div>
</template>

<script>
import Bus from '../../bus.js'
	export default{
		data(){
			return {
				checked:false,
				number:{
					allLenght:undefined,
					selectList:undefined
				}
			}
		},
		created() {
			Bus.$on('itemLength',(msg)=>{
				this.number.allLenght = msg
			})
			Bus.$on('itemSelecet',(msg)=>{
				this.number.selectList = msg
			})
		},
		methods:{
			delAll(){
				let isDel = confirm(`确认删除${this.number.selectList}项吗？`);
				if (isDel == true) {
					Bus.$emit('delete',true)
				}
			},
			selectAll(){
				this.checked = !this.checked
				Bus.$emit('selectAll',this.checked)
			}
		}
	}
</script>

<style>
	.footer{
		height: 50px;
		line-height: 50px;
		display:flex;
		align-items: center;
		justify-content: space-between;
	}
	.right-del{
		cursor: pointer;
		width: 20px;
		height: 20px;
	}
</style>