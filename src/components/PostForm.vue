<template>
	<form @submit.prevent>
		<h4>Создание поста</h4>
		<input
			v-model='post.title'
			class='post__input'
			type='text'
			placeholder='Название поста'
		>
		<input
			v-model='post.body'
			class='post__input'
			type='text'
			placeholder='Описание поста'
		>
		<MyButton
			class='btn'
			style='align-self: end'
			@click='createPost'
		>
			Создать
		</MyButton>
	</form>
</template>

<script>
	import MyButton from '@/components/UI/MyButton.vue';

	export default {
		components: { MyButton },
		data() {
			return {
				post: {
					title: '',
					body: ''
				}
			}
		},
		methods: {
			createPost() {
				this.post.id = crypto?.randomUUID()
				this.$emit('create', this.post)
				this.post = {
					title: '',
					body: ''
				}
			}
		}
	};
</script>

<style scoped>
form {
	display: flex;
	flex-direction: column;
}

	.post__input {
		width: 100%;
		border: 1px solid teal;
		padding: 10px 15px;
		margin-top: 15px;
	}
</style>