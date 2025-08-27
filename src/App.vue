<script>
import PostList from '@/components/PostList.vue';
import PostForm from '@/components/PostForm.vue';
import MyDialog from '@/components/UI/MyDialog.vue';
import MyButton from '@/components/UI/MyButton.vue';
import axios from 'axios';

 export default {
	 components: {
		 MyButton,
		 MyDialog,
		 PostForm, PostList
	 },
	 data() {
		 return {
			 posts: [],
			 dialogVisible: false,
			 isPostsLoading: false
		 }
	 },
	 methods: {
		 updatePosts(post) {
			 this.posts.push(post)
			 this.dialogVisible = false
		 },
		 removePost(post) {
			 this.posts = this.posts.filter(p => p.id !== post.id)
		 },
		 showDialog() {
			 this.dialogVisible = true
		 },
		 async fetchPosts() {
			 try {
				 this.isPostsLoading = true
				 const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
				 this.posts = await response.data
			 } catch (e) {
				 alert(e)
			 } finally {
				 this.isPostsLoading = false
			 }
		 }
	 },
	 mounted() {
		 this.fetchPosts()
	 }
 }
</script>

<template>
	<div class='app'>
		<h1>Страница с постами</h1>
		<MyButton @click='showDialog'>Создать пост</MyButton>
		<MyDialog v-model:show='dialogVisible'>
			<PostForm @create='updatePosts'/>
		</MyDialog>
		<PostList
			@remove='removePost'
			:data='{posts}'
			v-if='!isPostsLoading'
		/>
		<div v-else>Идет загрузка.....</div>
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