<template>
	<div class="container">
		<h1>About</h1>
		<img src="/img/test.jpg">
	</div>
</template>
<script>
import axios from '@nuxtjs/axios';

export default {
	name: 'posts',
	transition: 'bounce',
	// fetch ({ store, params }) {
	// 	return axios.get('http://localhost:1337/posts')
	// 		.then((res) => {
	// 			console.log(res.data);
	// 			store.commit('posts', res);
	// 		})
	// }
}
</script>

<style scoped>

</style>