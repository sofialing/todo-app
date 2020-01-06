<template>
	<section>
		<h1 class="mt-4 mb-3 h2 text-center">Todo List</h1>
		<ul v-if="todos.length" id="todos" class="my-3">
			<transition-group
				name="list"
				enter-active-class="animated fadeInUp"
				leave-active-class="animated fadeOutDown"
			>
				<li
					v-for="todo in todos"
					v-bind:key="todo.id"
					@click="updateStatus(todo.id, $event)"
				>
					<span>
						{{ todo.description }}
						<small class="d-block"
							>Created: {{ format(todo.created) }}</small
						>
					</span>

					<font-awesome-icon
						icon="trash-alt"
						@click="deleteTodo(todo.id)"
					/>
				</li>
			</transition-group>
		</ul>
		<p v-else class="text-center">Nothing to display</p>
	</section>
</template>

<script>
import moment from 'moment';

export default {
	name: 'TodoItems',
	props: ['todos'],
	methods: {
		deleteTodo(id) {
			this.$emit('del-todo', id);
		},
		updateStatus(id, event) {
			if (event.target.tagName === 'LI') {
				this.$emit('update-status', id);
			}
		},
		format(str) {
			return moment(str).format('dddd, MMMM Do YYYY, h:mm a');
		}
	}
};
</script>

<style scoped>
#todos {
	display: flex;
	flex-direction: column;
	padding-left: 0;
	margin-bottom: 0;
}

#todos li {
	background-color: #385359;
	border: 1px solid #1e3a40;
	color: #fff;
	display: flex;
	align-items: center;
	justify-content: space-between;
	margin-bottom: -1px;
	padding: 0.75rem 1.25rem;
	position: relative;
	cursor: pointer;
}

#todos li:first-child {
	border-top-left-radius: 0.25rem;
	border-top-right-radius: 0.25rem;
}

#todos li:last-child {
	margin-bottom: 0;
	border-bottom-right-radius: 0.25rem;
	border-bottom-left-radius: 0.25rem;
}
</style>
