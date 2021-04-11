<script context="module">
	export const prerender = true;
	export async function load({ fetch }) {
		const res = await fetch('https://api.mbl.archi/wp-json/wp/v2/pages?slug=info');
		return {
			props: {
				page: await res.json()
			}
		};
	}
</script>

<script>
	export let page;
	export let segment;
	import Header from '$lib/Header.svelte';
	import { onMount } from 'svelte';

	let x;
	let y;
	let z;
	onMount(async () => {
		x = Math.floor(Math.random() * 255);
		y = Math.floor(Math.random() * 255);
		z = Math.floor(Math.random() * 255);
	});
</script>

{#if segment === undefined}
	<Header {x} {y} {z}>
		{@html page[0].content.rendered}
	</Header>
{/if}

<main class="pt">
	<slot />
</main>
