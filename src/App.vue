<script>
import PostList from '@/components/PostList.vue';
import PostForm from '@/components/PostForm.vue';
import MyDialog from '@/components/UI/MyDialog.vue';
import MyButton from '@/components/UI/MyButton.vue';
import axios from 'axios';
import MySelect from '@/components/UI/MySelect.vue';
import MyInput from '@/components/UI/MyInput.vue';

 export default {
	 components: {
		 MyInput,
		 MySelect,
		 MyButton,
		 MyDialog,
		 PostForm, PostList
	 },
	 data() {
		 return {
			 posts: [],
			 dialogVisible: false,
			 isPostsLoading: false,
			 selectedSort: '',
			 page: 1,
			 limit: 10,
			 totalPages: 0,
			 sortOptions: [
				 {value: 'title', name: 'По названию'},
				 {value: 'body', name: 'По описанию'},
			 ],
			 searchQuery: ''
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
				 const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
					 params: {
						 _page: this.page,
						 _limit: this.limit
					 }
				 })
				 this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
				 this.posts = await response.data
			 } catch (e) {
				 alert(e)
			 } finally {
				 this.isPostsLoading = false
			 }
		 },
		 setCurrentPage(number) {
			 this.page = number
			 this.fetchPosts()
		 }
	 },
	 mounted() {
		 this.fetchPosts()
	 },
	 computed: {
		 sortedPosts() {
			 return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
		 },
		 sortedAndSearchedPosts() {
			 return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
		 }
	 },
	 watch: {
	 }
 }
</script>

<template>
	<div class='app'>
		<h1>Страница с постами</h1>
		<MyInput v-model='searchQuery' placeholder='Поиск...'/>
		<div class='app__buttons'>
			<MyButton @click='showDialog'>Создать пост</MyButton>
			<MySelect v-model='selectedSort' :options='sortOptions'/>
		</div>
		<MyDialog v-model:show='dialogVisible'>
			<PostForm @create='updatePosts'/>
		</MyDialog>
		<PostList
			@remove='removePost'
			:posts='sortedAndSearchedPosts'
			v-if='!isPostsLoading'
		/>
		<div v-else>Идет загрузка.....</div>
		<div class='page__wrapper'>
			<div
				v-for='pageNumber in totalPages'
				:key='pageNumber'
				class='page'
				:class="{
					'current-page': page === pageNumber
				}"
				@click='setCurrentPage(pageNumber)'
			>
				{{pageNumber}}
			</div>
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

	.app__buttons {
		display: flex;
		justify-content: space-between;
	}

	.page__wrapper {
		display: flex;
		margin-top: 15px;
	}

	.page {
		border: 1px solid black;
		padding: 10px;
		cursor: pointer;
	}

	.current-page {
		border: 2px solid green;
		pointer-events: none;
		cursor: none;
	}
</style>