<script lang="ts">
	import Hero from '$lib/components/Hero.svelte';

	const {data} = $props();

	let avatar: string;
	$inspect(data.user)
	
</script>

{#if data.user}
	
{:else}
	<Hero />
{/if}
