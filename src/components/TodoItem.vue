<template>
	<div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
		<p>
			<input type="checkbox" v-on:change="markCompleted">
			{{ todo.title }}
			<button @click="$emit('del-todo', todo.id)" class="del">&times;</button>
		</p>
	</div>
</template>

<script>
export default {
	name: 'TodoItem',
	props: ["todo"],
	methods: {
		markCompleted(){
			this.todo.completed = !this.todo.completed;
		}
	}
}
</script>

<style scoped>
.todo-item {
	padding: 15px;
	background: #CDCDCD;
}
.is-complete {
	text-decoration: line-through;
}
.del {
    background: #ff000f;
    color: #FFF;
    border: none;
    cursor: pointer;
    float: right;
    border-radius: 50%;
    font-size: 20px;
    line-height: 20px;
    width: 30px;
    height: 30px;
}
</style>