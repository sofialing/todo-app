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
import TodoItems from "../components/TodoItems";
import AddTodo from "../components/AddTodo";
import CompletedTodoItems from "../components/CompletedTodoItems";
import moment from "moment";
export default {
  name: "TodoList",
  components: {
    TodoItems,
    AddTodo,
    CompletedTodoItems
  },
  data() {
    return {
      todos: []
    };
  },
  mounted() {
    if (localStorage.getItem("todos")) {
      this.todos = JSON.parse(localStorage.getItem("todos"));
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
      localStorage.setItem("todos", parsed);
    }
  }
};
</script>
