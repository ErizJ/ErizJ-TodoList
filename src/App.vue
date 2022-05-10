<template>
  <div id="root">
	<div id="title">{{msg}}</div> 
	<hr>
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader :addTodo="addTodo"></MyHeader>
        <MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"></MyList>
        <MyFooter :todos="todos" :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo"></MyFooter>
      </div>
    </div>
  </div>

</template>

<script>
	import 'animate.css'
	import MyHeader from './components/MyHeader.vue'
	import MyList from './components/MyList.vue'
	import MyFooter from './components/MyFooter.vue'


export default {
	name: 'App',
	components: {
		MyHeader,
		MyList,
		MyFooter
		},
	data(){
		return {
			todos:JSON.parse(localStorage.getItem('todos')) || [],
			msg:'My Todo-List'
		}
	},
	watch:{
		todos:{
			handler(value){
				localStorage.setItem('todos', JSON.stringify(value))
			},
			deep:true
		}
	},
	methods:{
		addTodo(todoObj){
			this.todos.unshift(todoObj)
		},
		checkTodo(id){
			this.todos.forEach((todo) => {
				if(todo.id === id)
					todo.done = !todo.done
			});
		},
		updateTodo(id,title){
			this.todos.forEach((todo)=>{
				if(todo.id === id) todo.title = title
			})
		},
		deleteTodo(id){
			this.todos = this.todos.filter((todo)=>{
				return todo.id !== id
			})
		},
		checkAllTodo(done){
			this.todos.forEach((todo)=>{
				todo.done = done
			})
		},
		clearAllTodo(){
			this.todos = this.todos.filter((todo)=>{
				return !todo.done
			})
		}
	},
	mounted(){
		this.$bus.$on('updateTodo',this.updateTodo)
	},
	beforeDestroy(){
		this.$bus.$off('updateTodo')
	}
}
</script>

<style>
	#title{
		text-align: center;
		font-size: 40px;
		font-weight: bold;
		font-family: courier;
	}
	
	/*base*/
	body {
		background: #fff;
	}

	.btn {
		display: inline-block;
		padding: 4px 12px;
		margin-bottom: 0;
		font-size: 14px;
		line-height: 20px;
		text-align: center;
		vertical-align: middle;
		cursor: pointer;
		box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
		border-radius: 4px;
	}

	.btn-danger {
		color: #fff;
		background-color: #da4f49;
		border: 1px solid #bd362f;
	}
	
	.btn-edit {
		color: #fff;
		background-color: blue;
		border: 1px solid #2a357c;
		margin-right: 5px;
	}

	.btn-danger:hover {
		color: #fff;
		background-color: #bd362f;
	}

	.btn:focus {
		outline: none;
	}

	.todo-container {
		width: 600px;
		margin: 0 auto;
	}
	.todo-container .todo-wrap {
		padding: 10px;
		border: 1px solid #ddd;
		border-radius: 5px;
	}
  
</style>
