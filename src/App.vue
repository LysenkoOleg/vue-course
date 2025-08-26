<script>
import PostList from '@/components/PostList.vue';
import PostForm from '@/components/PostForm.vue';

 export default {
	 components: {
		 PostForm, PostList
	 },
	 data() {
		 return {
			 posts: [
				 {id: 1, title: 'Javascript', body: 'Описание поста'},
				 {id: 2, title: 'Javascript 2', body: 'Описание поста'},
				 {id: 3, title: 'Javascript 3', body: 'Описание поста'},
			 ],
		 }
	 },
	 methods: {
		 updatePosts(post) {
			 this.posts.push(post)
		 },
		 removePost(post) {
			 this.posts = this.posts.filter(p => p.id !== post.id)
		 }
	 }
 }
</script>

<template>
	<div class='app'>
		<PostForm @create='updatePosts'/>
		<PostList @remove='removePost' :data='{posts}'/>
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
</style>