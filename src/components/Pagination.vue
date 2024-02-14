<script setup>
	import { ref, computed, defineEmits } from 'vue';
	const emits = defineEmits(['prev', 'next']);
	const props = defineProps({
		items: {
			type: Array,
			required: true,
		},
		itemsPerPage: {
			type: Number,
			default: 5,
		},
		currentPage: {
			type: Number,
			required: true,
			default: 1,
		},
	});
	const totalPages = computed(() =>
		Math.ceil(props.items.length / props.itemsPerPage)
	);
	const nextPage = () => {
		if (props.currentPage < totalPages.value) {
			emits('next');
		}
	};

	const prevPage = () => {
		if (props.currentPage > 1) {
			emits('prev');
		}
	};
</script>

<template>
	<div class="px-4 mt-4 text-center">
		<button
			@click="prevPage"
			:disabled="props.currentPage === 1"
			:class="{
				'text-gray-400 cursor-not-allowed pointer-events-none':
					props.currentPage === 1,
			}"
		>
			{{ '<' }}
		</button>
		Page {{ props.currentPage }} / {{ totalPages }}
		<button
			@click="nextPage"
			:disabled="props.currentPage === totalPages"
			:class="{
				'text-gray-400 cursor-not-allowed pointer-events-none':
					props.currentPage === totalPages,
			}"
		>
			{{ '>' }}
		</button>
	</div>
</template>
