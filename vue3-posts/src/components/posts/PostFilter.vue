<template>
	<form @submit.prevent>
		<div class="row g-3 justify-content-center">
			<div class="col">
				<input
					:value="title_like"
					@input="$emit('update:title_like', $event.target.value)"
					type="text"
					class="form-control"
				/>
			</div>
			<div class="col-3">
				<select
					:value="limit"
					@input="$emit('update:limit', $event.target.value)"
					class="form-select"
				>
					<option value="3">3개씩 보기</option>
					<option value="6">6개씩 보기</option>
					<option value="9">9개씩 보기</option>
				</select>
			</div>
		</div>
	</form>
</template>

<script setup>
defineProps({
	limit: {
		type: Number,
	},
	title_like: {
		type: String,
	},
});

defineEmits(['update:title_like', 'update:limit']);
</script>

<style lang="scss" scoped></style>
