<template>
	<transition
	appear name="animate__animated animate__bounce"
	enter-active-class="animate__backInLeft"
	leave-active-class="animate__backOutLeft"
	>
		<li>
			<label>
				<input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)"/>
				<span v-show="!todo.isEdit">{{todo.title}}</span>
				<input
					v-show="todo.isEdit"
					type="text"
					:value="todo.title"
					@blur="handleBlur(todo,$event)"
					ref="inputTitle"
				/>
			</label>
			<button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
			<button v-show="!todo.isEdit" class="btn btn-edit" @click="handleEdit(todo)">编辑</button>
		</li>
	</transition>
</template>

<script>
export default {
    name:'MyItem',
	props:['todo','checkTodo','deleteTodo'],
	methods:{
		handleCheck(id){
			this.checkTodo(id)
		},
		handleDelete(id){
			if(confirm('确定要删除此代办吗？')){
				this.deleteTodo(id)
			}
		},
		handleEdit(todo){
			if(Object.prototype.hasOwnProperty.call(todo,'isEdit')){
				todo.isEdit = true
			}else{
				this.$set(todo,'isEdit',true)
			}
			
			this.$nextTick(function(){
				this.$refs.inputTitle.focus()
			})
		},
		handleBlur(todo,event){
			todo.isEdit = false
			console.log(event.target.value)
			if(!event.target.value.trim()){
				return alert('输入不能为空！！')
			}else{
				this.$bus.$emit('updateTodo',todo.id,event.target.value)
			}
		}
	}
}
</script>

<style scoped>
	/*item*/
	li {
		list-style: none;
		height: 36px;
		line-height: 36px;
		padding: 0 5px;
		border-bottom: 1px solid #ddd;
	}
	
	li label {
		float: left;
		cursor: pointer;
	}
	
	li label li input {
		vertical-align: middle;
		margin-right: 6px;
		position: relative;
		top: -1px;
	}
	
	li button {
		float: right;
		display: none;
		margin-top: 3px;
	}
	
	li:before {
		content: initial;
	}
	
	li:last-child {
		border-bottom: none;
	}
	
	li:hover{
		background-color: #262627;
	}
	
	li:hover button{
		display: block;
	}
</style>