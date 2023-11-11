<template>
	<form>
		<div class="mb-3">
			<label for="title" class="form-label">제목</label>
			<input
				type="text"
				:value="title"
				@input="$emit('update:title', $event.target.value)"
				class="form-control"
				id="title"
			/>
		</div>
		<div class="mb-3">
			<label for="content">내용</label>
			<textarea
				class="form-control"
				:value="content"
				@input="$emit('update:content', $event.target.value)"
				id="content"
				rows="3"
			></textarea>
		</div>
		<div class="d-flex gap-2 mt-4">
			<slot name="actions"> </slot>
		</div>
	</form>
</template>

<script setup>
defineProps({
	title: String,
	content: String,
});

defineEmits(['update:title', 'update:content']);
</script>

<style lang="scss" scoped></style>
