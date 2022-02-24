<template>
	<div class="user-page">
		<button class="btn btn-primary" @click="openModal">Подробнее</button>

		<AModal2
			v-if="isModalOpen"
			title="Пользовательское соглашение"
			@close="isModalOpen = false"
		>
		</AModal2>
	</div>
</template>

<script>
import AModal2 from './AModal2'

export default {
	components: { AModal2 },
	data() {
		return {
			isModalOpen: false,
		}
	},
	methods: {
		openModal() {
			this.isModalOpen = true
		},
	},
}
</script>

<style></style>
