<template>
	<div class='post'>
		<div>
			<div><strong>Название: </strong>{{ post.title}}</div>
			<div><strong>Описание: </strong>{{ post.body }}</div>
		</div>
		<div class='post__buttons'>
			<MyButton @click="$emit('remove', post)" class='btn'>Удалить</MyButton>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		post: {
			type: Object,
			required: true
		},
	}
};
</script>

<style scoped>
.post {
	display: flex;
	align-items: center;
	justify-content: space-between;
	padding: 15px;
	border: 2px solid teal;
	margin-block: 15px;
}
</style>