<template>
	<div>
		<h2>게시글 수정</h2>
		<hr class="my-4" />
		<PostForm
			v-model:title="posts.title"
			v-model:content="posts.content"
			@submit.prevent="edit"
		>
			<template #actions>
				<button
					type="button"
					class="btn btn-outline-dark"
					@click="goDetailPage"
				>
					취소
				</button>
				<button class="btn btn-primary">저장</button>
			</template>
		</PostForm>
	</div>
	<!-- <AppAlert :show="showAlert" :message="vAlertMessage" :type="alertType" /> -->
	<AppAlert :items="alerts" />
</template>

<script setup>
import { getPostById, updatePost } from '@/api/posts';
import { useRouter } from 'vue-router';
import { useRoute } from 'vue-router';
import { ref } from 'vue';
import PostForm from '@/components/posts/PostForm.vue';
import AppAlert from '@/components/AppAlert.vue';

const router = useRouter();
const route = useRoute();
const id = route.params.id;

const posts = ref({
	title: null,
	content: null,
});

const fetchPost = async () => {
	try {
		const { data } = await getPostById(id);
		posts.value = data;
	} catch (error) {
		console.log(error);
	}
};
fetchPost();

const edit = async () => {
	try {
		await updatePost(id, { ...posts.value });
		// router.push({ name: 'PostDetail', params: { id } });
		vAlert('수정이 완료되었습니다.', 'success');
	} catch (error) {
		console.log(error);
		vAlert('네트워크 오류', 'error');
	}
};

const goDetailPage = () => {
	router.push({
		name: 'PostDetail',
		params: {
			id,
		},
	});
};

// alert
// const showAlert = ref(false);
// const vAlertMessage = ref();
// const alertType = ref();
const alerts = ref([]);

const vAlert = (message, type) => {
	alerts.value.push({ message, type });
	// showAlert.value = true;
	// vAlertMessage.value = message;
	// alertType.value = type;
	setTimeout(() => {
		alerts.value.shift();
		// pop : 맨 뒷 값 제거, shift: 맨 앞 값 제거
		// showAlert.value = false;
	}, 3000);
};
</script>

<style lang="scss" scoped></style>
