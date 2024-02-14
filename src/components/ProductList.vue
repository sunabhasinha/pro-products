<script setup>
	import { reactive, ref, computed, watchEffect, watch } from 'vue';
	import Product from './Product.vue';
	import Pagination from './Pagination.vue';
	import productsItems from '../config.json';
	import ProductSynopsis from './ProductSynopsis.vue';
	import CustomButton from './CustomButton.vue';
	import CustomInput from './CustomInput.vue';

	const products = reactive(productsItems);

	function handleAccordion(selectedIndex) {
		paginatedItems.value?.forEach((product, index) => {
			product.isExpanded =
				index === selectedIndex ? !product.isExpanded : false;
		});
	}
	const currentPage = ref(1);
	const productNameToSearch = ref('');
	const filteredProducts = ref([]);
	const ITEMS_PER_PAGE = 10;

	const paginatedItems = computed(() => {
		const startIndex = (currentPage.value - 1) * ITEMS_PER_PAGE;
		const endIndex = startIndex + ITEMS_PER_PAGE;
		return products?.slice(startIndex, endIndex);
	});

	function searchProductByName(name) {
		if (!name) {
			filteredProducts.value = [];
			return;
		}
		filteredProducts.value = products.filter((product) =>
			product.name.toLowerCase().includes(name.toLowerCase())
		);
	}
	const displayedProducts = computed(() => {
		return filteredProducts.value.length > 0
			? filteredProducts.value
			: paginatedItems.value;
	});

	watchEffect(() => {
		if (!productNameToSearch.value) filteredProducts.value.length = 0;
	});
</script>

<template>
	<div
		class="flex flex-col justify-center items-center min-h-screen bg-gray-100"
	>
		<h1 class="text-3xl text-left mb-2 font-bold">Products</h1>
		<div class="w-[350px] p-4">
			<div class="flex justify-center items-center">
				<CustomInput
					:placeholder="'Find a Product'"
					:id="'product_text'"
					:type="'text'"
					class="my-2 w-3/4"
					@input="($event) => (productNameToSearch = $event)"
					:showLabel="false"
				/>
				<CustomButton
					class="w-1/4 ml-1 px-4 py-2 bg-gray-700 h-[40px] rounded-md text-white mb-0 text-center hover:bg-slate-500"
					@click="searchProductByName(productNameToSearch)"
					text="Search"
				/>
			</div>
			<div class="flex justify-center items-center">
				<CustomInput
					:placeholder="'Product Name'"
					:id="'product_name'"
					:type="'text'"
					class="my-2 w-3/5"
					:showLabel="false"
				/>
				<CustomButton
					class="w-2/5 ml-1 bg-green-900 mb-0 text-white rounded-md cursor-pointer hover:bg-green-700"
					text="Add Product"
				/>
			</div>
		</div>

		<div class="flex items-center justify-center bg-gray-100">
			<div class="p-4">
				<div v-for="(product, index) in displayedProducts" :key="product.name">
					<ProductSynopsis
						:product="product"
						:index="index"
						@handleAccordion="handleAccordion"
					/>
					<Product :product="product" />
				</div>
				<Pagination
					v-if="products.length"
					:currentPage="currentPage"
					@prev="currentPage--"
					@next="currentPage++"
					:items="products"
					:itemsPerPage="ITEMS_PER_PAGE"
				/>
			</div>
		</div>
	</div>
</template>
