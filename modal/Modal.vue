<template>
	<div class="modal fade show">
		<div class="modal-dialog">
			<div class="modal-content">
				<div class="modal-header">
					<h5 class="modal-title">
						{{ title }}
					</h5>
					<button
						type="button"
						class="close"
						aria-label="Close"
						@click="closeModal"
					>
						<span aria-hidden="true">&times;</span>
					</button>
				</div>
				<div class="modal-body" @scroll="onBodyScroll" ref="modalBody">
					<slot></slot>
				</div>
				<div class="modal-footer">
					<slot name="footer">
						<button type="button" class="btn btn-secondary" @click="closeModal">
							Отмена
						</button>
						<button
							type="button"
							class="btn btn-primary"
							:disabled="!isRulesReaded"
						>
							Принять
						</button>
					</slot>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		title: {
			type: String,
			required: '',
		},
	},
	data() {
		return {
			isRulesReaded: false,
		}
	},
	mounted() {
		const modalBody = this.$refs.modalBody
		modalBody.scrollTop = modalBody.scrollHeight - modalBody.clientHeight
	},

	methods: {
		closeModal() {
			this.$emit('close')
		},
		onBodyScroll() {
			const modalBody = this.$refs.modalBody
			if (
				modalBody.clientHeight + modalBody.scrollTop >=
				modalBody.scrollHeight
			) {
				this.isRulesReaded = true
			}
		},
	},
}
</script>

<style>
.modal {
	display: block;
}
.modal-body {
	height: 300px;
	overflow-y: scroll;
}
</style>
