<script setup>
	import { Collapse } from 'vue-collapsed';
	import CustomInput from './CustomInput.vue';
	import CustomImage from './CustomImage.vue';
	import CustomButton from './CustomButton.vue';
	const IMAGE_URL =
		'https://images.pexels.com/photos/302896/pexels-photo-302896.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1';

	const { product } = defineProps(['product']);
</script>

<template>
	<div class="px-4">
		<Collapse :when="product?.isExpanded">
			<div>
				<div class="flex justify-between items-center my-4">
					<CustomImage class="w-[200px] h-[200px]" :src="IMAGE_URL" />
					<div class="flex flex-col">
						<CustomButton
							text="Replace"
							class="px-4 py-1 bg-gray-700 rounded-sm text-white hover:bg-slate-500"
						/>
						<CustomButton
							class="px-4 py-2 bg-white rounded-md text-black"
							text="Clear"
						/>
					</div>
				</div>

				<CustomInput
					:label="'Image Title'"
					:placeholder="'Image Title'"
					:id="'img_title'"
					:type="'text'"
					class="my-2"
				/>
				<CustomInput
					:label="'Alt Text'"
					:placeholder="'Alt text'"
					:id="'alt_text'"
					:type="'text'"
					class="my-2"
				/>
				<CustomInput
					:label="'Link'"
					:placeholder="'Link'"
					:id="'link'"
					:type="'text'"
					class="my-2"
				/>
			</div>
		</Collapse>
	</div>
</template>
