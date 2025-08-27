<template>
	<div v-if='data.posts.length > 0'>
		<h3>Список постов</h3>
		<PostItem
			v-for='post in data.posts'
			:post='post'
			:key="post.id"
			@remove="$emit('remove', post)"
		/>
	</div>
	<h2 v-else style='color: red'>Список постов пуст</h2>
</template>

<script>
import PostItem from '@/components/PostItem.vue';

export default {
	components: {
		PostItem
	},
	props: {
		data: {
			required: true,
			posts: {
				type: Array,
			}
		}
	}
};
</script>

<style scoped>
</style>