<script>
	import favicon from '$lib/assets/favicon.svg';
    import lights from '$lib/images/christmas lights.png';
	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

{@render children()}

<img src="{lights}" alt="Christmas lights" />
