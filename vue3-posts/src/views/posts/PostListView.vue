<template>
	<div>
		<h2>게시글 목록</h2>
		<hr class="my-4" />
		<PostFilter
			:limit="params._limit"
			:title_like="params.title_like"
			@update:title_like="e => (params.title_like = e)"
			@update:limit="e => (params._limit = e)"
		>
		</PostFilter>
		<hr class="my-4" />
		<AppGrid :items="posts" colClass="col-4">
			<template v-slot="{ slotItem }">
				<PostItem
					:title="slotItem.title"
					:content="slotItem.content"
					:createdAt="slotItem.createdAt"
					@click="goPage(slotItem.id)"
				></PostItem>
			</template>
		</AppGrid>
		<AppPagination
			:currentPage="params._page"
			:pageCount="pageCount"
			@page="
				page => {
					params._page = page;
				}
			"
		/>
		<template v-if="posts && posts.length > 0">
			<hr class="my-4" />
			<AppCard>
				<PostDetailView :id="1"></PostDetailView>
			</AppCard>
		</template>
	</div>
</template>

<script setup>
import PostItem from '@/components/posts/PostItem.vue';
import PostDetailView from '@/views/posts/PostDetailView.vue';
import AppCard from '@/components/AppCard.vue';
import AppGrid from '@/components/AppGrid.vue';
import PostFilter from '@/components/posts/PostFilter.vue';
import { ref, computed, watchEffect } from 'vue';
import { getPosts } from '@/api/posts';
import { useRouter } from 'vue-router';
import AppPagination from '@/components/AppPagination.vue';
// import { useRouter } from 'vue-router';

const posts = ref([]);
const router = useRouter();
const params = ref({
	_sort: 'createdAt',
	_order: 'desc',
	_limit: '3',
	_page: 1,
	title_like: '',
});
// pagination
const totalCount = ref(0);
const pageCount = computed(() =>
	Math.ceil(totalCount.value / params.value._limit),
);

const fetchPost = async () => {
	try {
		const { data, headers } = await getPosts(params.value);
		posts.value = data;
		totalCount.value = headers['x-total-count'];
	} catch (error) {
		console.log(error);
	}
};
watchEffect(fetchPost);

const goPage = id => {
	router.push({
		name: 'PostDetail',
		params: {
			id,
		},
	});
};
</script>

<style lang="scss" scoped></style>
