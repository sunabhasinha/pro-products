<script setup>
	const {
		label,
		placeholder,
		id,
		type,
		disabled = false,
		required = false,
		showLabel = true,
	} = defineProps([
		'label',
		'placeholder',
		'id',
		'type',
		'disabled',
		'required',
		'showLabel',
	]);

	const emits = defineEmits(['input']);
	let inputValue = '';
	const handleChange = (event) => {
		inputValue = event.target.value;
		emits('input', inputValue);
	};
</script>
<template>
	<div>
		<label
			v-if="showLabel"
			:for="id"
			class="block mb-2 text-sm font-medium text-gray-900"
			>{{ label }}</label
		>
		<input
			:type="type"
			:aria-hidden="id"
			class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 hover:border-gray-700 hover:placeholder-gray-700"
			:placeholder="placeholder"
			:required="required"
			:disabled="disabled"
			v-model="inputValue"
			@input="handleChange"
		/>
	</div>
</template>
