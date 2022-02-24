<template>
	<input v-model="searchName" type="text" />
	<ul>
		<li v-for="(name, index) in matchName" :key="index">
			{{ name }}
		</li>
	</ul>
	<h4>total Name</h4>
	<ul>
		<li v-for="(name, index) in names" :key="index">
			{{ name }}
		</li>
	</ul>
</template>

<script>
export default {
	data() {
		return {
			names: ['Vasya333', 'Kolya1', 'Petya', 'Kolya2'],
			searchName: '',
		}
	},
	computed: {
		matchName() {
			return this.names.filter((name) =>
				name.toLowerCase().includes(this.searchName.toLowerCase())
			)
		},
	},
}
</script>

<style></style>
