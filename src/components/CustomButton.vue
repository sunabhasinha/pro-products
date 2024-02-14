<script setup>
	const { text } = defineProps(['text']);
</script>

<template>
	<button
		type="button"
		class="focus:ring-4 focus:ring-blue-300 text-sm px-5 py-2.5 me-2"
	>
		{{ text }}
	</button>
</template>
