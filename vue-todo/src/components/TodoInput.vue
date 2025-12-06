<template lang="html">
	<div>
		<input type="text" ref="todoInput" v-model="newTodoItem" @keyup.enter="addTodo" />
		<button type="button" @click="addTodo">add</button>
	</div>
</template>
<script>
export default {
	data() {
		return {
			newTodoItem: "",
		};
	},
	methods: {
		addTodo() {
			if (!this.newTodoItem.trim()) {
				this.$refs.todoInput.focus();
				return;
			}
			const obj = { completed: false, item: this.newTodoItem };
			localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
			this.clearInputAndFoucus();
		},
		clearInputAndFoucus() {
			this.newTodoItem = "";
			this.$refs.todoInput.focus();
		},
	},
};
</script>
<style lang=""></style>
