<template>
	<input
		class='post__input'
		type='text'
		:value='modelValue'
		@input='updateInput'
	/>
</template>

<script>
export default {
	name: 'MyInput',
	props: {
		modelValue: [String, Number]
	},
	methods: {
		updateInput(event) {
			this.$emit('update:modelValue', event.target.value)
		}
	}
};
</script>

<style scoped>
.post__input {
	width: 100%;
	border: 1px solid teal;
	padding: 10px 15px;
	margin-top: 15px;
}
</style>