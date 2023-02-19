<template>
	<div>
		<div
			ref="modal"
			class="modal fade"
			:class="[{ show: showModal, 'd-block': showModal }, modalClass]"
			tabindex="-1"
			role="dialog"
		>
			<div
				class="modal-dialog modal-dialog-centered"
				:class="modalSize"
				role="document"
			>
				<div class="modal-content">
					<div
						v-if="!hideHeader"
						class="modal-header"
						:class="isborderHeader ? 'border-bottom'  : 'border-bottom-0'"
					>
						<slot name="title"></slot>
						<button
							v-if="isborderHeader"
							type="button"
							class="btn-close"
							data-dismiss="modal"
							aria-label="Close"
							v-on:click="$emit('closeModal')"
						>
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x-lg" viewBox="0 0 16 16">
                            <path d="M2.146 2.854a.5.5 0 1 1 .708-.708L8 7.293l5.146-5.147a.5.5 0 0 1 .708.708L8.707 8l5.147 5.146a.5.5 0 0 1-.708.708L8 8.707l-5.146 5.147a.5.5 0 0 1-.708-.708L7.293 8 2.146 2.854Z"/>
                        </svg>
                        </button>
					</div>
					<div class="modal-body">
						<slot name="body"></slot>
					</div>
				</div>
			</div>
		</div>
		<div
			v-if="showModal"
			class="modal-backdrop fade show"
		></div>
	</div>

</template>

<script>
export default {
	name: "ModalC",
	emits: ["closeModal"],
	props: ["showModal", "modalClass", "isborderHeader", "modalSize", "hideHeader"],
	watch: {
		showModal: {
			handler(newVal) {
				if(!newVal) {
                    // eslint-disable-next-line
                    return this.showModal = newVal
                }

				const body = document.querySelector("body");
				this.showModal ? body.classList.add("modal-open"): body.classList.remove("modal-open");
			},
			immediate: true,
			deep: true,
		},
	},
	data() {
		return {};
	},
};
</script>

<style lang="scss" scoped>
.btn-close {
    border: none;
    background-color: transparent;
    padding: 0;
    margin: 0
}
</style>