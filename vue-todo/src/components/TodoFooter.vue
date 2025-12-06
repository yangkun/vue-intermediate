<template lang="html">
	<div>
		<button type="button" @click="clearAll">clear all</button>
	</div>
</template>
<script>
export default {
	methods: {
		clearAll() {
			const removeKeys = [];
			for (let i = 0, n = localStorage.length; i < n; i++) {
				const key = localStorage.key(i);
				console.log(key);
				if (!key.startsWith("_")) {
					removeKeys.push(key);
				}
			}
			removeKeys.forEach((k) => localStorage.removeItem(k));
		},
	},
};
</script>
