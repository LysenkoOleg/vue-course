<template>
	<button class='btn'>
		<slot></slot>
	</button>
</template>

<script>
export default {
name: 'MyButton'
};
</script>

<style scoped>
.btn {
	margin-top: 15px;
	background-color: transparent;
	color: teal;
	border: 1px solid teal;
	padding: 10px;
	cursor: pointer;
}
</style>