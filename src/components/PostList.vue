<template>
	<div>
		<h3>Список пользователей</h3>
		<PostItem
			v-for='post in data.posts'
			:post='post'
			:key="post.id"
			@remove="$emit('remove', post)"
		/>
	</div>
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