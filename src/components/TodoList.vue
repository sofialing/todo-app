<template>
	<main>
		<TodoItems
			v-bind:todos="notCompletedTodos"
			v-on:del-todo="deleteTodo"
			v-on:update-status="updateStatus"
		/>
		<AddTodo v-on:add-todo="addTodo" />
		<CompletedTodoItems
			v-bind:todos="completedTodos"
			v-on:del-todo="deleteTodo"
			v-on:update-status="updateStatus"
		/>
	</main>
</template>

<script>
import TodoItems from '../components/TodoItems';
import AddTodo from '../components/AddTodo';
import CompletedTodoItems from '../components/CompletedTodoItems';
import moment from 'moment';
export default {
	name: 'TodoList',
	components: {
		TodoItems,
		AddTodo,
		CompletedTodoItems
	},
	data() {
		return {
			todos: [
				// {
				// 	id: 0,
				// 	description: 'Have class meeting',
				// 	created: moment()
				// 		.subtract({ days: 5, minutes: 15, hours: 3 })
				// 		.calendar(),
				// 	completed: false,
				// 	completedTime: null
				// },
				// {
				// 	id: 1,
				// 	created: moment()
				// 		.subtract({ days: 2, minutes: 53, hours: 6 })
				// 		.calendar(),
				// 	description: 'Eat lunch',
				// 	completed: true,
				// 	completedTime: moment()
				// 		.subtract({ minutes: 15, hours: 3 })
				// 		.calendar()
				// },
				// {
				// 	id: 2,
				// 	created: moment()
				// 		.subtract({ days: 1, minutes: 23, hours: 14 })
				// 		.calendar(),
				// 	description: 'Code',
				// 	completed: true,
				// 	completedTime: moment().calendar()
				// },
				// {
				// 	id: 3,
				// 	created: moment()
				// 		.subtract({ minutes: 15, hours: 3 })
				// 		.calendar(),
				// 	description: 'Sleep',
				// 	completed: false,
				// 	completedTime: moment().calendar()
				// },
				// {
				// 	id: 4,
				// 	created: moment()
				// 		.subtract({ days: 31, minutes: 59, hours: 8 })
				// 		.calendar(),
				// 	description: 'Repeat',
				// 	completed: false,
				// 	completedTime: null
				// }
			]
		};
	},
	mounted() {
		if (localStorage.getItem('todos')) {
			this.todos = JSON.parse(localStorage.getItem('todos'));
		}
	},
	computed: {
		completedTodos() {
			return this.todos.filter(todo => todo.completed);
		},
		notCompletedTodos() {
			return this.todos.filter(todo => !todo.completed);
		}
	},
	methods: {
		addTodo(newTodo) {
			const { created, description, completed, completedTime } = newTodo;
			const id = this.todos.length
				? this.todos[this.todos.length - 1].id + 1
				: 0;
			this.todos.push({
				id,
				created,
				description,
				completed,
				completedTime
			});
			this.saveTodos();
		},
		deleteTodo(id) {
			this.todos = this.todos
				.filter(todo => todo.id !== id)
				.map((todo, index) => ({
					id: index,
					description: todo.description,
					completed: todo.completed
				}));
			this.saveTodos();
		},
		updateStatus(id) {
			this.todos[id].completed = !this.todos[id].completed;
			this.todos[id].completedTime = moment();
			this.saveTodos();
		},
		saveTodos() {
			const parsed = JSON.stringify(this.todos);
			localStorage.setItem('todos', parsed);
		}
	}
};
</script>
