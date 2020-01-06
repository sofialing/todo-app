<template>
	<div id="app" class="container my-5">
		<TodayInfo />
		<TodoList />
	</div>
</template>

<script>
import TodayInfo from './components/TodayInfo.vue';
import TodoList from './components/TodoList.vue';

export default {
	name: 'app',
	components: {
		TodayInfo,
		TodoList
	}
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Barlow+Semi+Condensed:400,600&display=swap');
@import 'https://cdn.jsdelivr.net/npm/animate.css@3.5.1';

body {
	background-color: #1e3a40;
	color: #ffffff;
	font-family: 'Barlow Semi Condensed', sans-serif;
}

.container {
	max-width: 450px;
}
</style>
