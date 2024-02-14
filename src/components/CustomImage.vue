<script setup>
	const { src, alt } = defineProps(['src', 'alt']);
</script>

<template>
	<img
		height="300"
		width="300"
		class="object-cover rounded-sm"
		:src="src"
		:alt="alt"
	/>
</template>
