<template>
	<input type="text" @input="updateInput" :value="modelValue" class="input" />
</template>

<script>
export default {
	name: 'my-input',
	props: {
		modelValue: [String, Number],
	},
	methods: {
		updateInput(event) {
			this.$emit('update:modelValue', event.target.value)
		},
	},
}
</script>

<style>
input {
	height: 25px;
}
</style>
