<script>
 export default {
	 data() {
		 return {
			 posts: [
				 {id: 1, title: 'Javascript', body: 'Описание поста'},
				 {id: 2, title: 'Javascript 2', body: 'Описание поста'},
				 {id: 3, title: 'Javascript 3', body: 'Описание поста'},
			 ],
			 title: '',
			 body: ''
		 }
	 },
	 methods: {
		 createPost() {
			 const newPost = {
				 id: crypto?.randomUUID(),
				 title: this.title,
				 body: this.body
			 }
			 this.posts.push(newPost)
			 this.title = ''
			 this.body = ''
		 },
	 }
 }
</script>

<template>
	<div class='app'>
		<form @submit.prevent>
			<h4>Создание поста</h4>
			<input
				v-bind:value='title'
				@input='title = $event.target.value'
				class='post__input'
				type='text'
				placeholder='Название поста'
			>
			<input
				v-bind:value='body'
				@input='body = $event.target.value'
				class='post__input'
				type='text'
				placeholder='Описание поста'
			>
			<button class='btn' @click='createPost'>Создать</button>
		</form>
		<div class='post' v-for='post in posts'>
			<div><strong>Название: </strong>{{ post.title }}</div>
			<div><strong>Описание: </strong>{{ post.body }}</div>
		</div>
	</div>
</template>

<style>
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	.app {
		padding: 20px;
	}

	.post {
		padding: 15px;
		border: 2px solid teal;
		margin-block: 15px;
	}

	form {
		display: flex;
		flex-direction: column;
	}

	.btn {
		margin-top: 15px;
		align-self: flex-end;
		background-color: transparent;
		color: teal;
		border: 1px solid teal;
		padding: 10px;
		cursor: pointer;
	}

	.post__input {
		width: 100%;
		border: 1px solid teal;
		padding: 10px 15px;
		margin-top: 15px;
	}
</style>