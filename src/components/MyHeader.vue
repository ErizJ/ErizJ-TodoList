<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" @keyup.enter="add" v-model="title"/>
  </div>
</template>

<script>
	import {nanoid} from 'nanoid'
	
	export default {
		name:'MyHeader',
		data(){
			return {
				title:''
			}
		},
		methods:{
			add(){
				if(this.title.trim()){
					const todoObj = {
						id:nanoid(),
						title:this.title,
						done:false
					}
					this.addTodo(todoObj)
					this.title = ''
				}
				else{
					alert('输入不能为空！')
				}
			}
		},
		props:['addTodo']
	}
</script>

<style scoped>
	/*header*/
	.todo-header input {
		width: 560px;
		height: 28px;
		font-size: 14px;
		border: 1px solid #ccc;
		border-radius: 4px;
		padding: 4px 7px;
	}
	
	.todo-header input:focus {
		outline: none;
		border-color: rgba(82, 168, 236, 0.8);
		box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
	}

	.todo-header{
		padding-bottom: 10px;
	}
</style>