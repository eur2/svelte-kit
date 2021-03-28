<script context="module">
	export const prerender = true;
	export async function load({ page, fetch }) {
		const res = await fetch(`https://api.mbl.archi/wp-json/wp/v2/posts?slug=${page.params.slug}`);
		return {
			props: {
				post: await res.json()
			}
		};
	}
</script>

<script>
	export let post;
	// console.log(post[0]);
</script>

<svelte:head>
	<title>{post[0].slug}</title>
</svelte:head>

<h1>{post[0].slug}</h1>
