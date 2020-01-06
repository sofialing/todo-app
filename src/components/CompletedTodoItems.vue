<template>
  <section v-show="todos.length" class="mt-4">
    <h1 class="mt-4 mb-3 h4 text-center">Completed</h1>
    <ul id="completed-todos">
      <transition-group
        name="list"
        enter-active-class="animated fadeInDown"
        leave-active-class="animated fadeOutUp"
      >
        <li v-for="todo in todos" v-bind:key="todo.id" @click="updateStatus(todo.id, $event)">
          <span>
            {{ todo.description }}
            <small class="d-block">Completed: {{ format(todo.completedTime) }}</small>
          </span>

          <font-awesome-icon icon="trash-alt" @click="deleteTodo(todo.id)" />
        </li>
      </transition-group>
    </ul>
  </section>
</template>

<script>
import moment from "moment";
export default {
  name: "CompletedTodoItems",
  props: ["todos"],
  methods: {
    deleteTodo(id) {
      // Send to parent
      this.$emit("del-todo", id);
    },
    updateStatus(id, event) {
      if (event.target.tagName === "LI") {
        this.$emit("update-status", id);
      }
    },
    format(str) {
      return moment(str).format("dddd, MMMM Do YYYY, h:mm a");
    }
  }
};
</script>

<style scoped>
#completed-todos {
  display: flex;
  flex-direction: column;
  padding-left: 0;
  margin-bottom: 0;
}

#completed-todos li {
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

#completed-todos li:first-child {
  border-top-left-radius: 0.25rem;
  border-top-right-radius: 0.25rem;
}

#completed-todos li:last-child {
  margin-bottom: 0;
  border-bottom-right-radius: 0.25rem;
  border-bottom-left-radius: 0.25rem;
}

#completed-todos li .fas {
  color: rgba(255, 255, 255, 0.5);
}

#completed-todos li {
  background: rgba(15, 34, 38, 0.5);
}

/* #completed-todos li span {
	text-decoration: line-through;
} */
</style>
