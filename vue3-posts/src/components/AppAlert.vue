<template>
	<!-- 트랜지션 -->
	<!-- <Transition name="slide">
		<div v-if="show" class="app-alert alert" role="alert" :class="styleClass">
			{{ message }}
		</div>
	</Transition> -->

	<!-- 트랜지션 그룹 -->
	<div class="app-alert">
		<TransitionGroup name="slide">
			<div
				v-for="({ message, type }, index) in items"
				:key="index"
				class="alert"
				:class="styleClass(type)"
				role="alert"
			>
				{{ message }}
			</div>
		</TransitionGroup>
	</div>
</template>

<script setup>
import { computed } from 'vue';
// transiton group
defineProps({
	items: Array,
});

const styleClass = type =>
	type === 'error' ? 'alert-danger' : 'alert-success';

// transition
// const props = defineProps({
// 	show: {
// 		type: Boolean,
// 		default: false,
// 	},
// 	message: {
// 		type: String,
// 		required: true,
// 	},
// 	type: {
// 		type: String,
// 		default: 'error',
// 		validator: value => ['success, error'].includes(value),
// 	},
// });

// const styleClass = computed(() =>
// 	props.type === 'error' ? 'alert-danger' : 'alert-success',
// );
</script>

<style scoped>
.app-alert {
	position: fixed;
	top: 10px;
	right: 10px;
}

.slide-enter-from,
.slide-leave-to {
	opacity: 0;
	transform: translateY(-30px);
}

.slide-enter-active,
.slide-leave-active {
	transition: all 0.5s ease;
}
.slide-enter-to,
.slide-leave-from {
	opacity: 1;
	transform: translateY(0);
}
</style>
