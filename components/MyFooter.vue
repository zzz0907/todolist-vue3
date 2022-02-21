<template>
    <div class="todo-footer">
		<label>
			<!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
			<input type="checkbox" v-model="isCheckAll"/>
		</label>
		<span>
			<span>已完成{{donetodo}}</span> / 全部{{total}}
		</span>
		<button class="btn btn-danger" @click="clearAllTodo" >清除已完成任务</button>
	</div>
</template>

<script>
import { computed } from '@vue/runtime-core'
export default {
    name:'MyFooter',
    props:['todos','checkAlltodo','clearAll'],
    setup(props) {
        // 总数
        const total=computed(()=>{
			return props.todos.length
			})
        //已完成的数 使用reduce方法做条件统计
        const donetodo = computed(()=>{
            return props.todos.reduce((pre,todo)=> pre + (todo.isCompleted ? 1 : 0) ,0) 
        })
        //控制全选框
        const isCheckAll = computed({
            get(){
                return donetodo.value === props.todos.length && total.value > 0
            },
            set(value){
                props.checkAlltodo(value)
            }
        })
        // 清除按钮
        function clearAllTodo(){
            props.clearAll()
        }

        
        return {
            total,
            donetodo,
            isCheckAll,
            clearAllTodo
            
        }
    }
}
</script>

<style >
    /*footer*/
	.todo-footer {
		height: 40px;
		line-height: 40px;
		padding-left: 6px;
		margin-top: 5px;
	}

	.todo-footer label {
		display: inline-block;
		margin-right: 20px;
		cursor: pointer;
	}

	.todo-footer label input {
		position: relative;
		top: -1px;
		vertical-align: middle;
		margin-right: 5px;
	}

	.todo-footer button {
		float: right;
		margin-top: 5px;
	}
</style>