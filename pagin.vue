<template>
	<div class="pages">
		<p>Pages {{ currentPage }} from {{ pages }}</p>

		<button @click="currentPage++">add</button>
		<button v-for="page in pages" @click="currentPage = page">
			{{ page }}
		</button>
		<button @click="currentPage--">dis</button>
	</div>
</template>
<script>
export default {
	data() {
		return {
			pages: 3,
			currentPage: 1,
		}
	},
}
</script>
<style>
.pages {
	display: flex;
}
</style>
