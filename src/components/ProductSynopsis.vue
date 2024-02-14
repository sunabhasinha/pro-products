<script setup>
	import CustomImage from './CustomImage.vue';

	const { product, index } = defineProps(['product', 'index']);

	const emits = defineEmits(['handleAccordion']);
	const status = Object.freeze({
		yellow: 'bg-yellow-500',
		red: 'bg-red-500',
		green: 'bg-green-500',
	});

	function handleAccordion() {
		emits('handleAccordion', index);
	}
</script>
<template>
	<div class="flex justify-between my-2 w-[350px] px-4">
		<div class="flex items-center">
			<CustomImage class="w-[32px] h-[32px] rounded-sm" :src="product.image" />
			<div
				class="rounded-full w-[10px] h-[10px] mx-4"
				:class="{ [status[product.status]]: true }"
			></div>
			<h4 class="w-[200px]">{{ product.name }}</h4>
		</div>
		<div>
			<span
				@click="handleAccordion"
				id="caret"
				class="cursor-pointer text-base"
				>{{ product.isExpanded ? '\u2304' : '\u2303' }}</span
			>
		</div>
	</div>
</template>
