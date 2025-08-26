<template>
	<div class='post'>
		<div>
			<div><strong>Название: </strong>{{ post.title}}</div>
			<div><strong>Описание: </strong>{{ post.body }}</div>
		</div>
		<div class='post__buttons'>
			<MyButton class='btn'>Удалить</MyButton>
		</div>
	</div>
</template>

<script>
import MyButton from '@/components/UI/MyButton.vue';

export default {
	components: { MyButton },
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