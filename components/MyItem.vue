<template>
    <li>
		<label>
			
            <input type="checkbox" :checked="todo.isCompleted" @change="handleCheck(todo.id)"/>
			<span>{{todo.title}}</span>
		</label>
		<button class="btn btn-danger" @click="delTodo">删除</button>
	</li>
</template>

<script>
export default {
    name:'MyItem',
    props:['todo','deleteTodo','checkTodo'],
    setup(props){
        const delTodo=()=>{
            if(window.confirm('确定删除吗？')){
                props.deleteTodo(props.todo.id)
            }
        }
        function handleCheck(id){
            props.checkTodo(id)
        }
    return{
        delTodo,
        handleCheck
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
		background-color: #ddd;
	}
	
	li:hover button{
		display: block;
	}
</style>