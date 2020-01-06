<template>
  <div id="app">
    <TodayInfo />
    <TodoList />
  </div>
</template>

<script>
import TodayInfo from "./components/TodayInfo.vue";
import TodoList from "./components/TodoList.vue";

export default {
  name: "app",
  components: {
    TodayInfo,
    TodoList
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Barlow+Semi+Condensed:400,600&display=swap");
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";

body {
  width: 100vw;
  height: 100vh;
  background-color: #1e3a40;
  color: #ffffff;
  font-family: "Barlow Semi Condensed", sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
}

#app {
  width: 100vw;
  padding: 1.5rem;
}

@media screen and (min-width: 450px) {
  #app {
    max-width: 414px;
  }
}
</style>
