<template>
	<form id="createNewTodo" class="text-center mt-4 mb-5" @submit.prevent="addTodo">
		<input
			class="form-control m-auto"
			type="text"
			placeholder="Add a new todo..."
			autocomplete="off"
			v-model="description"
		/>
	</form>
</template>

<script>
import moment from 'moment';

export default {
	name: 'AddTodo',
	data() {
		return {
			description: ''
		};
	},
	methods: {
		addTodo() {
			if (this.description.length === 0) {
				return;
			}
			const newTodo = {
				created: moment(),
				description: this.description.trim(),
				completed: false,
				completedTime: null
			};
			// Send to parent
			this.$emit('add-todo', newTodo);
			this.description = '';
		}
	}
};
</script>

<style scoped>
input[type='text'],
input[type='text']:focus {
	background-color: #385359;
	border: none;
	color: #fff;
	height: auto;
	padding: 0.75rem 1.25rem;
	max-width: 100%;
	margin: 0;
}

input[type='text']::placeholder {
	color: rgba(255, 255, 255, 0.75);
}
</style>
