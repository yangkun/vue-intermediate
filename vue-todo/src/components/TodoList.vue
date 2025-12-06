<template lang="html">
	<div>
		<ul class="list-group">
			<li v-for="(item, i) in todoItems" :key="i" class="list-group-item text-start">
				<i class="fas fa-check cursor-pointer mr-3" @click="toggleComplete(item.item)"></i>

				<span :class="{ completed: item.completed }">{{ item.item }}</span>

				<button type="button" @click="removeTodo(item.item)">delete</button>
			</li>
		</ul>
	</div>
</template>
<script>
export default {
	data() {
		return {
			todoItems: [],
		};
	},
	created() {
		this.fetchData();
	},
	methods: {
		fetchData() {
			this.todoItems = [];

			if (localStorage.length > 0) {
				for (let i = 0, n = localStorage.length; i < n; i++) {
					if (!localStorage.key(i).startsWith("_")) {
						const itemString = localStorage.getItem(localStorage.key(i));
						const obj = JSON.parse(itemString);
						this.todoItems.push(obj);
					}
				}
			}
		},
		removeTodo(item) {
			localStorage.removeItem(item);
			this.fetchData();
		},
		toggleComplete(item) {
			const itemString = localStorage.getItem(item);
			const obj = JSON.parse(itemString);
			obj.completed = !obj.completed;
			localStorage.setItem(item, JSON.stringify(obj));
			this.fetchData();
		},
	},
};
</script>
<style lang="css">
span.completed {
	color: #b4b4b4;
	text-decoration: line-through;
}
</style>
