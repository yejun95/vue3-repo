<template>
	<nav class="my-4" aria-label="Page navigation example">
		<ul class="pagination justify-content-center">
			<li class="page-item" :class="isPrevPage">
				<a
					class="page-link"
					href="#"
					aria-label="Previous"
					@click.prevent="$emit('page', currentPage - 1)"
				>
					<span aria-hidden="true">&laquo;</span>
				</a>
			</li>
			<li
				class="page-item"
				v-for="page in pageCount"
				:key="page"
				:class="{ active: currentPage === page }"
			>
				<a class="page-link" href="#" @click.prevent="$emit('page', page)">{{
					page
				}}</a>
			</li>
			<li class="page-item" :class="isNextPage">
				<a
					class="page-link"
					href="#"
					aria-label="Next"
					@click.prevent="$emit('page', currentPage + 1)"
				>
					<span aria-hidden="true">&raquo;</span>
				</a>
			</li>
		</ul>
	</nav>
</template>

<script setup>
import { computed } from 'vue';
const props = defineProps({
	currentPage: {
		type: Number,
		required: true,
	},
	pageCount: {
		type: Number,
		required: true,
	},
});

defineEmits(['page']);
// 부모에서 가져온 props 데이터를 자식에서 바꿀 수 없다.
// emit으로 올려서 부모에서 변경되게 만든다.

const isPrevPage = computed(() => {
	return { disabled: !(props.currentPage > 1) };
});
const isNextPage = computed(() => {
	return { disabled: !(props.currentPage < props.pageCount) };
});
</script>

<style lang="scss" scoped></style>
