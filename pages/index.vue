<template>
	<section class="container">
		<div>
			<logo/>
			<h1 class="title">
				nuxt-test
			</h1>
			<h2 class="subtitle">
				My riveting Nuxt.js project
			</h2>
			<div class="links">
				<a
					href="https://nuxtjs.org/"
					target="_blank"
					class="button--green">Documentation</a>
				<a
					href="https://github.com/nuxt/nuxt.js"
					target="_blank"
					class="button--grey">GitHub</a>
			</div>
			<h1 class="title">Posts</h1>
			<ul>
				<li v-for="{ id, title } in slicedPosts">
					{{ title }}
				</li>
			</ul>
			<nuxt-link to="/about">About</nuxt-link>
			<div class="links">
				<button @click="createPost" class="button--grey">
					Create a post (send POST request)
				</button>
			</div>
		</div>
	</section>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
	components: {
		Logo
	},
	transition: 'slide-left',
	data() {
		return {
			posts: []
		}
	},
	async asyncData(ctx) {
		return {
			posts: await ctx.app.$postRepository.index()
		}
	},
	computed: {
		slicedPosts() {
			return this.posts
		}
	},
	methods: {
		async createPost() {
			const result = await this.$postRepository.create({
				title: 'foo',
				body: 'bar',
				userId: 1
			});
			console.log(result);
			// Fix ids to be unique
			this.posts.push({ ...result, id: Number(this.posts.slice(-1)[0].id) + 1 })
		}
	},

}
</script>

<style scoped>

	.title {
		font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
		'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
		display: block;
		font-weight: 300;
		font-size: 100px;
		color: #35495e;
		letter-spacing: 1px;
	}

	.subtitle {
		font-weight: 300;
		font-size: 42px;
		color: #526488;
		word-spacing: 5px;
		padding-bottom: 15px;
	}

	.links {
		padding-top: 15px;
	}
</style>
