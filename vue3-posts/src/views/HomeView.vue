<template>
	<h1>HomeView</h1>
	<p>{{ $route.path }}</p>
	<button class="btn btn-primary" @click="$router.push('/about')">
		About으로 이동
	</button>
	<hr class="my-4" />
	<AppGrid :items="items" v-slot="{ slotItem }" colClass="col-4">
		<AppCard>{{ slotItem }}</AppCard>
	</AppGrid>
</template>

<script setup>
import { ref } from 'vue';
import AppCard from '@/components/AppCard.vue';
import AppGrid from '@/components/AppGrid.vue';

const items = ref(['건의', '희재', '득권', '유진']);
</script>

<style lang="scss" scoped></style>
