<template>
	<div id="newTasksBlock">
		<input
			@keyup.enter="add_new()"
			type="text"
			name=""
			id=""
			v-model="nametask"
			placeholder="Введите новую задачу"
			maxlength="23"
		/>
		<br />
		<p id="p_name_task">Задача будет называться:<br />{{ nametask }}</p>
		<button @click="add_new()">Добавить</button>
	</div>
	<div id="block_ready_posts">
		<div v-for="(item, index) in items" :key="item.id" class="block_posts">
			
			<p v-if="item.status === 'active'">{{ item.title }}</p>
			<p class="text_closed" v-if="item.status !== 'active'">{{ item.title }}</p>
			<br />
			<button v-if="item.status !== 'active'" @click="returns(index)" class="button_green">Восстановить</button>
			<button v-if="item.status === 'active'" @click="close(index)" class="button_green">Завершить</button><br />
			<button @click="delete_block(index)" class="button_red">Удалить</button>
		</div>
	</div>
</template>

<script setup>
import { ref } from 'vue';
const items = ref([]);
function add_new() {
	items.value.push({ title: nametask.value, status: 'active' },);
	nametask.value = '';
}

function delete_block(number){
	items.value.splice(number, 1);
}
function close(number){
	var status_button;
	var value_title = items.value[number].title;
	console.log(value_title);
	items.value.splice(number, 1);
	items.value.push({title: value_title, status: 'none'})
	console.log(status_button);
}
function returns(number){
	var status_button;
	var value_title = items.value[number].title;
	console.log(value_title);
	items.value.splice(number, 1);
	items.value.push({title: value_title, status: 'active'})
	console.log(status_button);
}
const nametask = ref('');
</script>

<style scoped>
button:hover {
	cursor: pointer;
	text-decoration: underline;
}
#newTasksBlock {
	padding: 20px;
	text-align: center;
	display: block;
	margin-left: auto;
	margin-right: auto;
	border: 2px solid rgb(204, 204, 204);
	max-width: max-content;
	border-radius: 20px;
	margin-top: 30px;
}
#newTasksBlock input {
	font-size: 20px;
	padding: 10px;
	border-radius: 20px;
	border: 2px solid rgb(204, 204, 204);
}
#newTasksBlock button {
	padding: 10px;
	border-radius: 20px;
	background-color: green;
	color: white;
	font-size: 20px;
	margin-top: 20px;
	padding-left: 40px;
	padding-right: 40px;
	border: none;
}
#newTasksBlock button:hover {
	cursor: pointer;
	text-decoration: underline;
}
#p_name_task {
	margin-top: 20px;
	font-size: 20px;
}
.block_posts {
	text-align: center;
	display: block;
	margin-left: auto;
	margin-right: auto;
	font-size: 30px;
	border-radius: 20px;
	margin-top: 20px;
	flex-direction: column;
	padding: 20px;
	border: 2px solid rgb(204, 204, 204);
	max-width: 400px;
}
.block_posts .button_red {
	background-color: rgb(192, 31, 31);
	color: white;
	font-size: 20px;
	padding: 10px;
	border-radius: 20px;
	border: none;
	margin-bottom: 30px;
}
.block_posts .button_green {
	background-color: green;
	color: white;
	font-size: 20px;
	padding: 10px;
	border-radius: 20px;
	border: none;
	margin-bottom: 15px;
	margin-top: 20px;
}
.text_closed{
	text-decoration: line-through;
}
</style>
