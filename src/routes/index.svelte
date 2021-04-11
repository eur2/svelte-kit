<script context="module">
	export const prerender = true;
	export const router = false;

	export async function load({ fetch }) {
		const res = await fetch('https://api.mbl.archi/wp-json/wp/v2/posts?_embed&per_page=100');
		return {
			props: {
				posts: await res.json()
			}
		};
	}
</script>

<script>
	export let posts;

	import Post from '$lib/Post.svelte';
</script>

<svelte:head>
	<title>MBL</title>
</svelte:head>
{#each posts as post}
	<Post
		slug={post.slug}
		title={post.title.rendered}
		phrase={post.acf.phrase}
		description={post.acf.description}
		year={post.acf.year}
		budget={post.acf.budget}
		area={post.acf.area}
		team={post.acf.team}
		program={post.acf.program}
		client={post.acf.client}
		status={post.acf.status}
		location={post.acf.location}
		video={post.acf.video}
		images={post.acf.images}
	/>
{/each}
