<template>
  <div class="todo-container">
			<div class="todo-wrap">
				<MyHeader :addTodo="addTodo"/>
				<MyList :todos="todos" :deleteTodo="deleteTodo" :checkTodo="checkTodo"/>
				<MyFooter :todos="todos" :checkAlltodo="checkAlltodo" :clearAll="clearAll"/>
			</div>
		</div>
</template>

<script>
import {reactive,toRefs} from 'vue'
import MyHeader from './components/MyHeader.vue'
import MyFooter from './components/MyFooter.vue'
import MyList from './components/MyList.vue'

export default {
  name: 'App',
  components: {
    MyHeader,
    MyFooter,
    MyList
  },
  setup() {
    const state = reactive({
      todos:[
        {id:'1',title:'吃饭',isCompleted:false},
        {id:'2',title:'睡觉',isCompleted:false},
        {id:'3',title:'打豆豆',isCompleted:true},
      ] ,
    })
    // 添加数据
    function addTodo(todo) {
      state.todos.unshift(todo)
    }
    // 删除数据
    function deleteTodo(id){
      state.todos = state.todos.filter( todo => todo.id !== id )
    }
    // 勾选数据
    function checkTodo(id){
      state.todos.forEach((todo)=>{
					if(todo.id === id) todo.isCompleted = !todo.isCompleted
				})
      
    }
    // 全选按钮
    function checkAlltodo(isCompleted){
				state.todos.forEach((todo)=>{
					todo.isCompleted = isCompleted
				})
			}
    // 清除所有按钮
    function clearAll(){
      state.todos = state.todos.filter((todo)=>{
					return !todo.isCompleted
				})
    }
    return{
      ...toRefs(state),
      addTodo,
      deleteTodo,
      checkTodo,
      checkAlltodo,
      clearAll
    }
  }
}
</script>

<style>
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
